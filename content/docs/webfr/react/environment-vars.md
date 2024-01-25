---
weight: 999
title: "Environment vars"
description: ""
icon: "article"
date: "2023-10-27T20:42:12+02:00"
lastmod: "2023-10-27T20:42:12+02:00"
draft: false
toc: true
---

## Adding Custom Environment Variables

[Docs](https://create-react-app.dev/docs/adding-custom-environment-variables/)

> The environment variables are embedded during the build time. 

### Example

```js
render() {
  return (
    <div>
      <small>You are running this application in <b>{process.env.NODE_ENV}</b> mode.</small>
      <form>
        <input type="hidden" defaultValue={process.env.REACT_APP_NOT_SECRET_CODE} />
      </form>
    </div>
  );
}

// Renders to:

<div>
    <small>You are running this application in <b>development</b> mode.</small>
    <form>
        <input type="hidden" value="abcdef" />
    </form>
</div>
```

## Referencing Environment Variables in the HTML

```js
<title>%REACT_APP_WEBSITE_NAME%</title>
```

> Apart from a few built-in variables (NODE_ENV and PUBLIC_URL), variable names must start with REACT_APP_ to work.

## Adding Temporary Environment Variables In Your Shell

**Windows (cmd.exe)**

```bash
set "REACT_APP_NOT_SECRET_CODE=abcdef" && npm start
(Note: Quotes around the variable assignment are required to avoid a trailing whitespace.)
```

**Windows (Powershell)**

```bash
($env:REACT_APP_NOT_SECRET_CODE = "abcdef") -and (npm start)
```

**Linux, macOS (Bash)**

```bash
REACT_APP_NOT_SECRET_CODE=abcdef npm start
```


## Adding Development Environment Variables In .env

To define permanent environment variables, create a file called .env in the root of your project:

```js
REACT_APP_NOT_SECRET_CODE=abcdef
```

### What other .env files can be used?

```
.env: Default.
.env.local: Local overrides. This file is loaded for all environments except test.
.env.development, .env.test, .env.production: Environment-specific settings.
.env.development.local, .env.test.local, .env.production.local: Local overrides of environment-specific settings.
```








