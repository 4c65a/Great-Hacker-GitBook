# GitHub Dorks para Encontrar Información Sensible

## **Tool**

[**https://github.com/techgaun/github-dorks**](https://github.com/techgaun/github-dorks)

[**https://github.com/tillson/git-hound**](https://github.com/tillson/git-hound)

[**https://github.com/BishopFox/GitGot**](https://github.com/BishopFox/GitGot)

[**https://github.com/hisxo/gitGraber**](https://github.com/hisxo/gitGraber)



### 🗂️ Archivos y Configuraciones Comunes

<pre class="language-git"><code class="lang-git">path:**/.git
<strong>path:**/.npmrc _auth
</strong>path:**/.dockercfg auth
path:**/.bash_history
path:**/.bash_profile aws
path:**/.sh_history
path:**/sftp-config.json
path:**/sftp.json
path:**/secrets.yml password
path:**/.esmtprc password
path:**/passwd
path:**/shadow
path:**/dbeaver-data-sources.xml
path:**/config.php dbpasswd
path:**/configuration.php JConfig password
path:**/wp-config.php
path:**/proftpdpasswd
path:**/.pgpass
path:**/idea14.key
path:**/hub oauth_token
path:**/.git-credentials
path:**/.htpasswd
path:**/.env
path:**/.env.production
path:**/.env.local
path:**/.env.development
path:**/credentials.json
path:**/firebase.json
path:**/settings.py SECRET_KEY
path:**/config.js apiKey
path:**/config.json apiKey
path:**/local.properties
path:**/gradle.properties
path:**/secrets.json
path:**/secrets.yml
path:**/docker-compose.yml
path:**/docker-compose.override.yml
path:**/docker-compose.prod.yml
path:**/docker-compose.dev.yml
path:**/docker-compose.test.yml
path:**/docker-compose.ci.yml
path:**/docker-compose.staging.yml
path:**/docker-compose.local.yml
path:**/.env.example
path:**/.env.sample
path:**/.env.backup
path:**/.env.bak
path:**/config.json password
path:**/config.yaml password
path:**/settings.ini password
path:**/credentials.yml password
path:**/secrets.env
path:**/secrets.txt
path:**/secrets.conf
path:**/secret.key
path:**/secret_token.rb
path:**/secrets.py
path:**/secrets.js
path:**/secrets.php
path:**/secrets.rb
path:**/secrets.go
path:**/secrets.swift
path:**/secrets.kt
path:**/secrets.scala
path:**/secrets.ts
path:**/secrets.rs
path:**/secrets.dart
path:**/secrets.elixir
path:**/secrets.clj
path:**/secrets.hs
path:**/secrets.vb
path:**/secrets.cs
path:**/secrets.cpp
path:**/secrets.c
path:**/secrets.asm
path:**/secrets.r
path:**/secrets.pl
path:**/secrets.lua
path:**/secrets.groovy
path:**/secrets.erl
path:**/secrets.pas
path:**/secrets.dpr
path:**/secrets.adb
path:**/secrets.pro
path:**/secrets.lisp
path:**/secrets.scm
path:**/secrets.ml
path:**/secrets.fs
path:**/secrets.coffee
path:**/secrets.elm
path:**/secrets.cr
path:**/secrets.nim
path:**/secrets.re
path:**/secrets.st
path:**/secrets.vala
path:**/secrets.zig
path:**/secrets.pony
path:**/secrets.janet
path:**/secrets.gleam
path:**/secrets.grain
path:**/secrets.roc
path:**/secrets.bsq
path:**/secrets.carbon
path:**/secrets.dark
path:**/secrets.dsp
path:**/secrets.flink
path:**/secrets.hydra
path:**/secrets.ink
path:**/secrets.jl
path:**/secrets.kojo
path:**/secrets.livecode
path:**/secrets.mod
path:**/secrets.obr
path:**/secrets.plk
path:**/secrets.quorum
path:**/secrets.rexx
path:**/secrets.sage
path:**/secrets.terra
path:**/secrets.uni
path:**/secrets.v
path:**/secrets.vhdl
path:**/secrets.xojo
path:**/secrets.xtend

</code></pre>

***

### 👤 Nombres de Usuario y Correos Electrónicos

```git
user:name
org:name type:users
in:login
in:name
fullname:firstname lastname
in:email
```

***

### 🧠 Dorks por Lenguaje de Programación

```git
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

```git
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

```git
aws_access_key_id
aws_secret_access_key
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
GCP_API_KEY
AZURE_SUBSCRIPTION_KEY
```

## 📡 Servicios de terceros (comunes en integraciones)

```git
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

```git
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

```git
smtp_password
smtp_user
smtp_username
gmail_password
gmail_username
```

## 🔒 Contraseñas, credenciales y hashes

```git
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

```git
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

```git
mysql_password
postgres_password
mongodb_password
oracle_password
conn.login
connection_string
```

## 🔧 Configs comunes

```git
auth
authentication
authorizationToken
encryption_key
bucket_password
```

## 🔍 Otros útiles para búsquedas

```git
"api token"
"db_password"
"connectionstring"
"access_key_id="
"access_key_secret="
"access_token="
```

***

