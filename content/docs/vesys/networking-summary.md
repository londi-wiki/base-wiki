---
weight: 999
title: "Networking Summary"
description: ""
icon: "article"
date: "2024-02-26T08:48:44+01:00"
lastmod: "2024-02-26T08:48:44+01:00"
draft: false
toc: true
---

## Netstat client/server

```bash
netstat -n
```

Nur mit diesem Befehl sieht man nicht wer der Client/Server ist.

```bash
netstat -a -n
```

## Verbindung passive schliessen

- Socket (s) auf fhnw.ch:80 aufmachen
- sout(s)

`netstat -a -n` zeigt dies als "ESTABLISHED" an

Irgendwann schliesst der Server die Verbindung (aktiv schliessen). Dies zeigt der Client als "CLOSE_WAIT" an.

## InputSteam.read()

```java
Socket s = server.accept();
int n = s.getInputStream().read();
// liest nur ein Byte ein.
```

## Socket auf Port öffnen welcher nicht offen ist

- Socket auf fhnw.ch:1234 öffnen 

nach einem timeout von ~20 Sekunden: `ConnectExpection`


## OutputStream close()

- Verbindung auf fhnw.ch:80
- getOutputStream
- out.write("GET / HTTP/1.0\r\n\r\n".getBytes())
- danach: getInputStream in
- BufferedReader(new InputStreamReader(in))
- Zeile für Zeile die Antwort lesen

Antwort: 

Theoretisch: Moved Permanently: 301 - "HTTP/1.1 301 Moved Permanently"

Aber: Das Verwenden von OutputStream in einem try-with, schliesst den OutputStream 
am Schluss des try-with was auch den Socket schliesst.

> out.close() schliesst ebenfalls den Socket.

## readLine()

- Server öffnet Socket
  - Ohne try-with also ohne auto close
  - Server sendet ein Zeichen aber ohne "\r\n"
- Client öffnet einen Socket
  - Liest eine Zeile `readLine()`

Programm terminiert nicht


## shutdownInput()

- Server öffnet Socket
  - InputStream().read()
- Client öffnet Socket
  - shutdownInput() ohne etwas zu schreiben
  - BufferedReader.readLine

Keine Ausgabe: Programm blockiert im `read()`


## Mehrere InputStreams

- Server öffnet Socket
  - schreibt: "012345..."
  - ohne try-with oder close()
- Client öffnet Socket
  - in1 = BufferedInputStream(s.getInputStream())
  - in2 = s.getInputStream() 
  - in1.read() > "1"
  - in2.read() > nichts... Das Programm blockiert hier sogar

Antwort: 1

> Würde der Server ein "close()" aufrufen, kommt trotzdem nur "1" heraus aber das Programm terminiert.

## isConnected()

- Server öffnet Socket
  - try-with
  - InputStream
    - while(isConnected)
      - printLn
- Client öffnet Socket
  - 

Antwort: isConnected gibt "true" zurück, solange die Verbindung lokal nicht geschlossen wird.
Wenn der Client resp. die Gegenstelle die Verbindung schliesst, ist isConnected **nach wie vor true**. 
Der InputStream gibt dann unendlich "-1" aus.

Also: "48, 49, ..., -1, -1, ..." (Ascii Code)

## flush()

- Client öffnet Socket mit try-with
  - BufferedOutputStream(s.getOutputStream())
  - out.write(0x01)
- Server öffnet Socket
  - var s = server.accept()
  - getInputStream.read()

Antwort: -1

Weil: BufferedOutputStream verwendet wurde. In so einem Fall muss out.flush() 
aufgerufen werden ODER der BufferedOutputStream in das try-with integriert werden. 

out.write(...) kann nach wie vor in das try { ... } geschrieben werden. 
Erst am Schluss wird automatisch "flush()" und danach close() aufgerufen.

## connection reset

- Server öffnet socket
  - 
- Client öffnet socket
  - 


## Formatter flush()

Gegeben:

```java
try (Formatter formatter = new Formatter(out)) {
    for (int i = 0; i < n; i++) {
        formatter.format(msg, i);
    }
    s.close();
    System.out.println("done.");
}
```

Lösung 1:

```java
try (Formatter formatter = new Formatter(out)) {
    for (int i = 0; i < n; i++) {
        formatter.format(msg, i);
    }
    formatter.flush();
    s.close();
    System.out.println("done.");
}
```

Lösung 2:

```java
try (s; Formatter formatter = new Formatter(out)) {
    for (int i = 0; i < n; i++) {
        formatter.format(msg, i);
    }
    System.out.println("done.");
}
```

Grund: 

Der Formatter braucht den BufferedWritter in welchem die DEFAULT_MAX_BUFFER_SIZE gesetzt ist.

```java
public Formatter(OutputStream os) {
        this(Locale.getDefault(Locale.Category.FORMAT),
             new BufferedWriter(new OutputStreamWriter(os)));
}

...

public BufferedWriter(Writer out) {
    this(out, initialBufferSize(), DEFAULT_MAX_BUFFER_SIZE);
}
```

Die `MAX_BYTE_BUFFER_CAPACITY` dient hier als Obergrenze für den Buffer. 
Deshalb kann bei der gegebenen Aufgabe die Ausgabe nicht vollständig gemacht werden.

```java
public final class StreamEncoder extends Writer {

    private static final int INITIAL_BYTE_BUFFER_CAPACITY = 512;
    private static final int MAX_BYTE_BUFFER_CAPACITY = 8192;
    
    ...

}
```





