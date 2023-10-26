---
description: https://www.exploit-db.com/google-hacking-database?category=1
---

# Files Containing Passwords

```
intitle:"Index of" htpasswd
```

```
intitle:"Index of" pwd.db
```

```
site:rentry.co intext:"password"
```

```
site:controlc.com intext:"password"
```

```
intext:"index of" "uploads"
```

```
intext:"password" | "passwd" | "pwd" site:ghostbin.com
```

```
site:pastebin.com intext:username | password | SECRET_KEY
```

```
inurl:/wp-content/uploads/ ext:txt "username" | "user name" | "uname" | "user" | "userid" | "user id" AND "password" | "pass word" | "pwd" | "pw"
```

```
intitle:"index of" "passwrod*"
```

```
intitle:"index of" "credentials"
```

```
"index of /" +passwd
```

```
intitle: "Index of ftp passwords"
```

```
Inurl: "login" Intitle:index of username and pass
```

```
filetype:log username admin
```

```
inurl:/wp-content/uploads/data.txt
```

```
allintext:"*.@gmail.com" OR "password" OR "username" filetype:xlsx
```

```
inurl:/wp-content/uploads/ ext:txt "username" AND "password" | "pwd" | "pw"
```

```
site:*.blob.core.windows.net ext:xls | ext:xlsx (login | password | username)
```

```
"public $user =" | "public $password = " | "public $secret =" | "public $db =" ext:txt | ext:log -git
```

```
intitle:"index of" "application-users.properties" | "mgmt-users.properties" | "*standalone.xml"
```

```
"insert into users" "VALUES" ext:sql | ext:txt | ext:log | ext:env
```

```
"define('SECURE_AUTH_KEY'" + "define('LOGGED_IN_KEY'" + "define('NONCE_KEY'" ext:txt | ext:cfg | ext:env | ext:ini
```

```
"keystorePass=" ext:xml | ext:txt -git -gitlab
```

```
intitle:"index of" "config.exs" | "dev.exs" | "test.exs" | "prod.secret.exs"
```

```
jdbc:mysql://localhost:3306/ + username + password ext:yml | ext:javascript -git -gitlab
```

```
jdbc:postgresql://localhost: + username + password ext:yml | ext:java -git -gitlab	jdbc:oracle://localhost: + username + password ext:yml | ext:java -git -gitlab
```

```
"db.username" + "db.password" ext:properties
```

```
"admin_password" ext:txt | ext:log | ext:cfg
```

```
ext:txt intext:@yahoo.com intext:password
```

```
intitle:"index of" "credentials.yml"
```

```
intitle:"index of" "passwords.yml"
```

```
intext:"username=" AND "password=" ext:log
```

```
intitle:"index of" "db.conf"
```

```
"contrasena" filetype:sql -github.com
```

```
intext:"@gmail.com" intext:"password" inurl:/files/ ext:txt
```

```
intitle:"index of" "ftp.passwd"
```

```
intitle:"index of" "htpasswd.txt"
```

```
"pass" "usuario" filetype:sql
```

```
intext:"aspx" filetype:txt login & password
```

```
inurl:login.txt filetype:txt
```
