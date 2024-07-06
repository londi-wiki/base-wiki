---
weight: 999
title: "Rest Client Generator"
description: ""
icon: "article"
date: "2024-03-25T10:42:20+01:00"
lastmod: "2024-03-25T10:42:20+01:00"
draft: false
toc: true
---

## Rest Client anhand openapi Spezifikation erstellen


Download [openapi-generator-cli](https://mvnrepository.com/artifact/org.openapitools/openapi-generator-cli/7.4.0)

### List

`java -jar .\openapi-generator-cli-7.4.0.jar list`

Output (25.03.2024)

```bash
CLIENT generators:
    - ada
    - android
    - apex
    - bash
    - c
    - clojure
    - cpp-qt-client
    - cpp-restsdk
    - cpp-tiny (beta)
    - cpp-tizen
    - cpp-ue4 (beta)
    - crystal (beta)
    - csharp
    - dart
    - dart-dio
    - eiffel
    - elixir
    - elm
    - erlang-client
    - erlang-proper
    - go
    - groovy
    - haskell-http-client
    - java
    - java-helidon-client (beta)
    - java-micronaut-client (beta)
    - javascript
    - javascript-closure-angular
    - javascript-flowtyped
    - jaxrs-cxf-client
    - jetbrains-http-client (experimental)
    - jmeter
    - julia-client (beta)
    - k6 (beta)
    - kotlin
    - lua (beta)
    - n4js (beta)
    - nim (beta)
    - objc
    - ocaml
    - perl
    - php
    - php-dt (beta)
    - php-nextgen (beta)
    - powershell (beta)
    - python
    - python-pydantic-v1
    - r
    - ruby
    - rust
    - scala-akka
    - scala-gatling
    - scala-pekko
    - scala-sttp
    - scala-sttp4 (beta)
    - scalaz
    - swift-combine
    - swift5
    - typescript (experimental)
    - typescript-angular
    - typescript-aurelia
    - typescript-axios
    - typescript-fetch
    - typescript-inversify
    - typescript-jquery
    - typescript-nestjs (experimental)
    - typescript-node
    - typescript-redux-query
    - typescript-rxjs
    - xojo-client
    - zapier (beta)


SERVER generators:
    - ada-server
    - aspnetcore
    - cpp-pistache-server
    - cpp-qt-qhttpengine-server
    - cpp-restbed-server
    - cpp-restbed-server-deprecated
    - csharp-functions
    - erlang-server
    - fsharp-functions (beta)
    - fsharp-giraffe-server (beta)
    - go-echo-server (beta)
    - go-gin-server
    - go-server
    - graphql-nodejs-express-server
    - haskell
    - haskell-yesod (beta)
    - java-camel
    - java-helidon-server (beta)
    - java-inflector
    - java-micronaut-server (beta)
    - java-msf4j
    - java-pkmst
    - java-play-framework
    - java-undertow-server
    - java-vertx-web (beta)
    - java-wiremock (beta)
    - jaxrs-cxf
    - jaxrs-cxf-cdi
    - jaxrs-cxf-extended
    - jaxrs-jersey
    - jaxrs-resteasy
    - jaxrs-resteasy-eap
    - jaxrs-spec
    - julia-server (beta)
    - kotlin-server
    - kotlin-spring
    - kotlin-vertx (beta)
    - nodejs-express-server (beta)
    - php-laravel
    - php-lumen
    - php-mezzio-ph
    - php-slim4
    - php-symfony
    - python-aiohttp
    - python-blueplanet
    - python-fastapi (beta)
    - python-flask
    - ruby-on-rails
    - ruby-sinatra
    - rust-axum (beta)
    - rust-server
    - scala-akka-http-server (beta)
    - scala-finch
    - scala-http4s-server
    - scala-lagom-server
    - scala-play-server
    - scalatra
    - spring


DOCUMENTATION generators:
    - asciidoc
    - cwiki
    - dynamic-html
    - html
    - html2
    - markdown (beta)
    - openapi
    - openapi-yaml
    - plantuml (beta)


SCHEMA generators:
    - avro-schema (beta)
    - graphql-schema
    - ktorm-schema (beta)
    - mysql-schema
    - postman-collection (beta)
    - protobuf-schema (beta)
    - wsdl-schema (beta)


CONFIG generators:
    - apache2
```


### Generate

`java -jar openapi-generator-cli-7.4.0.jar generate -i http://localhost:8080/api/openapi.json -g python-fastapi -o python-fastapi`

