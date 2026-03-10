# MCP Server für claude.ai mit Cloudflare Workers & Wrangler

Ein eigener MCP Server (Model Context Protocol) erlaubt es, Claude mit eigenen Tools zu erweitern – zum Beispiel um Web-Apps direkt aus dem Chat heraus zu deployen. Cloudflare Workers ist dafür eine ideale Plattform: kostenlos, global verteilt, und mit Wrangler einfach zu deployen.

## Was ist MCP?

MCP (Model Context Protocol) ist ein offenes Protokoll von Anthropic das es Claude erlaubt, externe Tools aufzurufen. Der Server läuft als HTTP-Dienst und antwortet auf JSON-RPC Nachrichten. Claude kommuniziert mit dem Server um herauszufinden welche Tools verfügbar sind, und ruft sie dann bei Bedarf auf.

Der Flow sieht so aus:

```
claude.ai → MCP Server (HTTP/JSON-RPC) → Externe API (z.B. Netlify, GitHub, ...)
```

---

## Projektstruktur

Ein minimaler Wrangler-basierter MCP Server besteht aus nur zwei Dateien:

```
mein-mcp/
├── worker.js       # Der eigentliche MCP Server Code
└── wrangler.toml   # Cloudflare-Konfiguration
```

---

## wrangler.toml

```toml
name = "mein-mcp-server"
main = "worker.js"
compatibility_date = "2024-11-01"
compatibility_flags = ["nodejs_compat"]

# Secrets NIE hier eintragen – immer via CLI:
# wrangler secret put MEIN_SECRET
```

Wichtig: `nodejs_compat` aktiviert Node.js-kompatible APIs wie `crypto` im Worker.

---

## MCP Protokoll Grundstruktur

Claude kommuniziert über JSON-RPC 2.0. Der Server muss drei Methoden unterstützen:

```
initialize          → Handshake, Protokollversion aushandeln
tools/list          → Claude fragt welche Tools verfügbar sind
tools/call          → Claude ruft ein konkretes Tool auf
```

Minimales Grundgerüst eines Workers:

```javascript
export default {
  async fetch(request, env) {
    const url = new URL(request.url);

    // CORS für claude.ai
    if (request.method === "OPTIONS") {
      return new Response(null, {
        headers: {
          "Access-Control-Allow-Origin": "*",
          "Access-Control-Allow-Methods": "POST, GET, OPTIONS",
          "Access-Control-Allow-Headers": "Content-Type, Authorization",
        },
      });
    }

    if (url.pathname === "/mcp" && request.method === "POST") {
      const { id, method, params } = await request.json();

      if (method === "initialize") {
        return respond(id, {
          protocolVersion: "2024-11-05",
          capabilities: { tools: {} },
          serverInfo: { name: "mein-mcp", version: "1.0.0" },
        });
      }

      if (method === "tools/list") {
        return respond(id, { tools: TOOLS });
      }

      if (method === "tools/call") {
        const result = await callTool(params.name, params.arguments, env);
        return respond(id, result);
      }
    }
  },
};

function respond(id, result) {
  return new Response(JSON.stringify({ jsonrpc: "2.0", id, result }), {
    headers: { "Content-Type": "application/json", "Access-Control-Allow-Origin": "*" },
  });
}
```

---

## Tools definieren

Jedes Tool braucht einen Namen, eine Beschreibung und ein JSON Schema für die Inputs:

```javascript
const TOOLS = [
  {
    name: "mein_tool",
    description: "Kurze, klare Beschreibung was das Tool tut – Claude liest das!",
    inputSchema: {
      type: "object",
      properties: {
        eingabe: {
          type: "string",
          description: "Was der Parameter bewirkt",
        },
      },
      required: ["eingabe"],
    },
  },
];
```

> **Tipp:** Die `description` ist entscheidend – Claude entscheidet anhand davon ob und wann es das Tool aufruft. Präzise Beschreibungen führen zu besseren Ergebnissen.

Das Tool gibt ein `content`-Array zurück:

```javascript
async function callTool(name, args, env) {
  if (name === "mein_tool") {
    const result = await machIrgendwas(args.eingabe);
    return {
      content: [{ type: "text", text: `Ergebnis: ${result}` }],
    };
  }
  throw new Error(`Unbekanntes Tool: ${name}`);
}
```

---

## OAuth 2.0 für claude.ai Connectors

Claude.ai unterstützt im Browser nur OAuth als Authentifizierungsmethode. Für einen persönlichen Single-User MCP Server kann man OAuth selbst im Worker implementieren – kein externer Provider nötig.

### Benötigte Endpoints

```
GET  /.well-known/oauth-authorization-server   → Discovery
GET  /oauth/authorize                           → Login-Formular anzeigen
POST /oauth/authorize                           → Passwort prüfen, Code ausstellen
POST /oauth/token                               → Code gegen Access Token tauschen
```

### Discovery Endpoint

Claude.ai ruft diesen Endpoint automatisch auf um die OAuth-URLs zu finden:

```javascript
if (url.pathname === "/.well-known/oauth-authorization-server") {
  return json({
    issuer: baseUrl,
    authorization_endpoint: `${baseUrl}/oauth/authorize`,
    token_endpoint: `${baseUrl}/oauth/token`,
    response_types_supported: ["code"],
    grant_types_supported: ["authorization_code"],
    code_challenge_methods_supported: ["S256"],
  });
}
```

### PKCE (Proof Key for Code Exchange)

Claude.ai verwendet PKCE (S256) beim OAuth Flow. Der Worker muss den `code_verifier` gegen den `code_challenge` validieren:

```javascript
// Beim Token-Exchange prüfen:
const hash = await crypto.subtle.digest("SHA-256", new TextEncoder().encode(code_verifier));
const computed = btoa(String.fromCharCode(...new Uint8Array(hash)))
  .replace(/\+/g, "-").replace(/\//g, "_").replace(/=/g, "");

if (computed !== gespeicherter_code_challenge) {
  return json({ error: "invalid_grant" }, 400);
}
```

### Tokens selbst signieren (HMAC)

Ohne externe Auth-Library kann man Tokens mit HMAC-SHA256 selbst signieren:

```javascript
async function signToken(payload, secret) {
  const data = JSON.stringify(payload);
  const key = await crypto.subtle.importKey(
    "raw", new TextEncoder().encode(secret),
    { name: "HMAC", hash: "SHA-256" }, false, ["sign"]
  );
  const sig = await crypto.subtle.sign("HMAC", key, new TextEncoder().encode(data));
  const sigHex = Array.from(new Uint8Array(sig))
    .map(b => b.toString(16).padStart(2, "0")).join("");
  return btoa(data) + "." + sigHex;
}
```

### In claude.ai eintragen

| Feld | Wert |
|------|------|
| MCP Server URL | `https://mein-mcp.NAME.workers.dev/mcp` |
| OAuth Client ID | beliebiger String (z.B. `claude-ai`) |
| OAuth Client Secret | beliebiger String (wird nicht geprüft) |

Client ID und Secret sind bei Single-User OAuth irrelevant – die echte Authentifizierung passiert über das Passwort im Login-Formular.

---

## Secrets verwalten mit Wrangler

Secrets werden verschlüsselt bei Cloudflare gespeichert und sind im Worker als `env.SECRET_NAME` zugänglich. **Niemals in `wrangler.toml` eintragen!**

```bash
# Secret setzen (interaktiv)
wrangler secret put MEIN_SECRET

# Secret auflisten (zeigt nur Namen, nicht Werte)
wrangler secret list

# Secret löschen
wrangler secret delete MEIN_SECRET
```

Im Worker zugänglich als:

```javascript
export default {
  async fetch(request, env) {
    const wert = env.MEIN_SECRET; // ✅
  }
};
```

---

## Wrangler – Nützliche Befehle & Tipps

### Deployment

```bash
# Lokal entwickeln (hot reload, kein echtes Deployment)
wrangler dev

# In Production deployen
wrangler deploy

# Bestimmte Umgebung deployen (z.B. staging)
wrangler deploy --env staging
```

### Logs & Debugging

```bash
# Live-Logs aus Production streamen (sehr nützlich!)
wrangler tail

# Mit Filter
wrangler tail --filter-status error
```

### Mehrere Umgebungen (wrangler.toml)

```toml
name = "mein-mcp"
main = "worker.js"
compatibility_date = "2024-11-01"

[env.staging]
name = "mein-mcp-staging"

[env.production]
name = "mein-mcp-production"
vars = { LOG_LEVEL = "error" }
```

### KV Storage (Key-Value Datenbank)

Für einfache Datenpersistenz ohne externe DB:

```toml
# wrangler.toml
[[kv_namespaces]]
binding = "MEIN_KV"
id = "abc123..."
```

```javascript
// Im Worker
await env.MEIN_KV.put("schlüssel", "wert");
const wert = await env.MEIN_KV.get("schlüssel");
```

KV erstellen:

```bash
wrangler kv namespace create MEIN_KV
```

### Cron Jobs

```toml
# wrangler.toml
[triggers]
crons = ["0 * * * *"]  # Jede Stunde
```

```javascript
export default {
  async scheduled(event, env, ctx) {
    // Wird vom Cron aufgerufen
  },
  async fetch(request, env) {
    // Normaler HTTP Handler
  }
};
```

### Limits (Free Tier)

| Resource | Limit |
|----------|-------|
| Requests/Tag | 100.000 |
| CPU-Zeit pro Request | 10ms |
| Worker-Grösse | 1 MB |
| KV Reads/Tag | 100.000 |
| KV Writes/Tag | 1.000 |

> **Tipp:** Die 10ms CPU-Zeit klingt wenig, gilt aber nur für reine CPU-Arbeit. Wartezeit auf externe APIs (fetch) zählt nicht dazu – ideal für MCP Server die hauptsächlich APIs weiterleiten.

---

## Praxisbeispiel: Netlify Deploy MCP

Ein vollständiger MCP Server der HTML-Prototypen auf Netlify deployt. Der Deploy-Prozess nutzt Netlify's file-digest API:

```javascript
async function deployWebapp({ html, site_name }, netlifyToken) {
  // 1. Neue Site erstellen
  const site = await netlifyFetch("/sites", {
    method: "POST",
    body: JSON.stringify(site_name ? { name: site_name } : {}),
  }, netlifyToken);

  // 2. SHA-1 Hash der Datei berechnen (Netlify braucht das)
  const htmlBytes = new TextEncoder().encode(html);
  const hashBuffer = await crypto.subtle.digest("SHA-1", htmlBytes);
  const sha1 = Array.from(new Uint8Array(hashBuffer))
    .map(b => b.toString(16).padStart(2, "0")).join("");

  // 3. Deploy mit file-digest anlegen
  const deploy = await netlifyFetch(`/sites/${site.id}/deploys`, {
    method: "POST",
    body: JSON.stringify({ files: { "/index.html": sha1 }, async: false }),
  }, netlifyToken);

  // 4. Datei hochladen
  await fetch(`https://api.netlify.com/api/v1/deploys/${deploy.id}/files/index.html`, {
    method: "PUT",
    headers: {
      Authorization: `Bearer ${netlifyToken}`,
      "Content-Type": "application/octet-stream",
    },
    body: htmlBytes,
  });

  return {
    content: [{
      type: "text",
      text: `✅ Deployt: ${site.ssl_url || site.url}\n🆔 Site-ID: ${site.id}`,
    }],
  };
}
```

---

## Checkliste: MCP Server für claude.ai

- [ ] `wrangler.toml` mit `compatibility_flags = ["nodejs_compat"]`
- [ ] CORS Headers für alle Responses (inkl. OPTIONS)
- [ ] `/.well-known/oauth-authorization-server` Discovery Endpoint
- [ ] OAuth `/authorize` (GET + POST) mit Login-Formular
- [ ] OAuth `/token` mit PKCE S256 Validierung
- [ ] Bearer Token Validierung vor jedem `/mcp` Call
- [ ] `initialize`, `tools/list`, `tools/call` JSON-RPC Methoden
- [ ] Secrets via `wrangler secret put` gesetzt (nie in `wrangler.toml`)
- [ ] Health-Check Endpoint `GET /` für einfaches Testen
