---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Github-Dorks

## **Tool**

[**https://github.com/techgaun/github-dorks**](https://github.com/techgaun/github-dorks)

[**https://github.com/tillson/git-hound**](https://github.com/tillson/git-hound)

[**https://github.com/BishopFox/GitGot**](https://github.com/BishopFox/GitGot)

[**https://github.com/hisxo/gitGraber**](https://github.com/hisxo/gitGraber)

## GitHub Dorks para Encontrar Información Sensible

### 🗂️ Archivos y Configuraciones Comunes

```bash
filename:manifest.xml
filename:travis.yml
filename:vim_settings.xml
filename:database
filename:prod.exs NOT prod.secret.exs
filename:prod.secret.exs
filename:.npmrc _auth
filename:.dockercfg auth
filename:WebServers.xml
filename:.bash_history
filename:.bash_profile aws
filename:.sh_history
filename:sftp-config.json
filename:sftp.json path:.vscode
filename:secrets.yml password
filename:.esmtprc password
filename:passwd path:etc
filename:shadow path:etc
filename:dbeaver-data-sources.xml
filename:config.php dbpasswd
filename:configuration.php JConfig password
filename:wp-config.php
filename:proftpdpasswd
filename:.pgpass
filename:idea14.key
filename:hub oauth_token
filename:.git-credentials
filename:.htpasswd
filename:.env
filename:.env.production
filename:.env.local
filename:.env.development
filename:credentials.json
filename:firebase.json
filename:settings.py SECRET_KEY
filename:config.js apiKey
filename:config.json apiKey
filename:local.properties
filename:gradle.properties
filename:secrets.json
filename:secrets.yml
filename:docker-compose.yml
filename:docker-compose.override.yml
filename:docker-compose.prod.yml
filename:docker-compose.dev.yml
filename:docker-compose.test.yml
filename:docker-compose.ci.yml
filename:docker-compose.staging.yml
filename:docker-compose.local.yml
filename:docker-compose.prod.override.yml
filename:docker-compose.dev.override.yml
filename:docker-compose.test.override.yml
filename:docker-compose.ci.override.yml
filename:docker-compose.staging.override.yml
filename:docker-compose.local.override.yml
filename:docker-compose.override.prod.yml
filename:docker-compose.override.dev.yml
filename:docker-compose.override.test.yml
filename:docker-compose.override.ci.yml
filename:docker-compose.override.staging.yml
filename:docker-compose.override.local.yml
filename:docker-compose.override.prod.override.yml
filename:docker-compose.override.dev.override.yml
filename:docker-compose.override.test.override.yml
filename:docker-compose.override.ci.override.yml
filename:docker-compose.override.staging.override.yml
filename:docker-compose.override.local.override.yml
filename:docker-compose.override.override.yml
filename:.env.example
filename:.env.sample
filename:.env.backup
filename:.env.bak
filename:config.json password
filename:config.yaml password
filename:settings.ini password
filename:credentials.yml password
filename:secrets.env
filename:secrets.txt
filename:secrets.conf
filename:secret.key
filename:secret_token.rb
filename:secrets.py
filename:secrets.js
filename:secrets.php
filename:secrets.rb
filename:secrets.go
filename:secrets.swift
filename:secrets.kt
filename:secrets.scala
filename:secrets.ts
filename:secrets.rs
filename:secrets.dart
filename:secrets.elixir
filename:secrets.clj
filename:secrets.hs
filename:secrets.m
filename:secrets.vb
filename:secrets.cs
filename:secrets.cpp
filename:secrets.c
filename:secrets.asm
filename:secrets.m
filename:secrets.r
filename:secrets.pl
filename:secrets.lua
filename:secrets.groovy
filename:secrets.erl
filename:secrets.f
filename:secrets.pas
filename:secrets.dpr
filename:secrets.adb
filename:secrets.pro
filename:secrets.lisp
filename:secrets.scm
filename:secrets.ml
filename:secrets.fs
filename:secrets.coffee
filename:secrets.elm
filename:secrets.cr
filename:secrets.nim
filename:secrets.re
filename:secrets.reb
filename:secrets.st
filename:secrets.vala
filename:secrets.zig
filename:secrets.pony
filename:secrets.janet
filename:secrets.gleam
filename:secrets.grain
filename:secrets.roc
filename:secrets.bsq
filename:secrets.carbon
filename:secrets.dark
filename:secrets.dsp
filename:secrets.flink
filename:secrets.hydra
filename:secrets.ink
filename:secrets.jl
filename:secrets.kojo
filename:secrets.livecode
filename:secrets.mod
filename:secrets.obr
filename:secrets.plk
filename:secrets.quorum
filename:secrets.rexx
filename:secrets.sage
filename:secrets.terra
filename:secrets.uni
filename:secrets.v
filename:secrets.vhdl
filename:secrets.xojo
filename:secrets.xtend
```

***

### 👤 Nombres de Usuario y Correos Electrónicos

```
user:name
org:name type:users
in:login
in:name
fullname:firstname lastname
in:email
```

***

### 🧠 Dorks por Lenguaje de Programación

```
language:python username
language:php username
language:sql username
language:html password
language:perl password
language:shell username
language:java api
language:javascript api
language:ruby password
language:go token
language:swift secret
language:kotlin key
language:scala credentials
language:typescript auth
language:rust password
language:dart api
language:elixir token
language:clojure secret
language:haskell key
language:objective-c credentials
language:vb.net password
language:c# token
language:c++ secret
language:c key
language:assembly credentials
language:matlab password
language:r token
language:perl secret
language:lua key
language:groovy credentials
language:erlang password
language:fortran token
language:pascal secret
language:delphi key
language:ada credentials
language:prolog password
language:lisp token
language:scheme secret
language:ocaml key
language:f# credentials
language:coffeescript password
language:elm token
language:crystal secret
language:nim key
language:reason credentials
language:rebol password
language:smalltalk token
language:vala secret
language:zig key
language:pony credentials
language:janet password
language:gleam token
language:grain secret
language:roc key
language:bosque credentials
language:carbon password
language:dark token
language:faust secret
language:flink key
language:hydra credentials
language:ink password
language:julialang token
language:kojo secret
language:livecode key
language:modula-2 credentials
language:oberon password
language:plankalkül token
language:quorum secret
language:rexx key
language:sage credentials
language:terra password
language:unicon token
language:verilog secret
language:vhdl key
language:xojo credentials
language:xtend password
language:zig token
```

***

## 🔑 Autenticación general y claves de API

```
api_key
apikey
api_token
api_secret
apiSecret
authorization_bearer:
auth_token
access_token
access_key
access_key_id
access_key_secret
secret_key
private_key
public_key
application_key
client_id
client_secret
consumer_key
token
```

## ☁️ Plataformas cloud comunes

```
aws_access_key_id
aws_secret_access_key
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
GCP_API_KEY
AZURE_SUBSCRIPTION_KEY
```

## 📡 Servicios de terceros (comunes en integraciones)

```
GITHUB_TOKEN
GITLAB_TOKEN
BITBUCKET_TOKEN
TRAVIS_TOKEN
CIRCLECI_TOKEN
HEROKU_API_KEY
NETLIFY_AUTH_TOKEN
VERCEL_AUTH_TOKEN
FIREBASE_API_KEY
SENDGRID_API_KEY
MAILGUN_API_KEY
TWILIO_API_KEY
STRIPE_API_KEY
PAYPAL_API_KEY
SLACK_API_TOKEN
DISCORD_API_TOKEN
TELEGRAM_BOT_TOKEN
```

## 🌐 Redes sociales y plataformas

```
FACEBOOK_API_KEY
GOOGLE_API_KEY
YOUTUBE_API_KEY
TWITTER_API_KEY
LINKEDIN_API_KEY
DROPBOX_API_KEY
SPOTIFY_API_KEY
REDDIT_API_KEY
TUMBLR_API_KEY
TIKTOK_API_KEY
SNAPCHAT_API_KEY
PINTEREST_API_KEY
INSTAGRAM_API_KEY
```

## 📧 Email y SMTP

```
smtp_password
smtp_user
smtp_username
gmail_password
gmail_username
```

## 🔒 Contraseñas, credenciales y hashes

```
password
passwd
passcode
secret
credentials
db_password
database_password
ftp_password
redis_password
ssh_password
ldap_password
keyPassword
OTP
password_hash
```

## 👤 Usuarios y logins

```
username
user
user_password
user_pass
dbuser
database_user
ftp_user
redis_user
ssh_user
```

## 💾 Bases de datos

```
mysql_password
postgres_password
mongodb_password
oracle_password
conn.login
connection_string
```

## 🔧 Configs comunes

```
auth
authentication
authorizationToken
encryption_key
bucket_password
```

## 🔍 Otros útiles para búsquedas

```
"api token"
"db_password"
"connectionstring"
"access_key_id="
"access_key_secret="
"access_token="
```

***

