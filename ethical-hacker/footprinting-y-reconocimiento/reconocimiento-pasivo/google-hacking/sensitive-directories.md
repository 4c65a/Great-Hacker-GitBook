---
description: https://www.exploit-db.com/google-hacking-database?category=1
---

# Sensitive Directories

```
intitle:Index of "/venv"
```

```
intitle:Index of "pyvenv.cfg"
```

```
site:com intitle:index of ..................etcpasswd
```

```
intitle:"index of /" "sqlite.db"
```

```
intitle:"index of" ".env"
```

```
intitle: "index of backup.php"
```

```
intitle:"index of" "private/log"
```

```
intitle: "Index of" inurl:fileadmin
```

```
intitle:index.of (inurl:admin | intitle:admin)
```

```
intitle:"index of" "/configs"
```

```
intitle:"index of" intext:"client.key.pem"
```

```
inurl:/wp-content/uploads/wp-file-manager-pro/fm_backup
```

```
inurl:wp-content/uploads/ intitle:logs
```

```
inurl:/wp-content/uploads/wp-file-manager-pro
```

```
"-----BEGIN EC PRIVATE KEY-----" | " -----BEGIN EC PARAMETERS-----" ext:pem | ext:key | ext:txt
```

```
"-----BEGIN PGP PRIVATE KEY BLOCK-----" ext:pem | ext:key | ext:txt -git
```

```
inurl:tcpconfig.html
```

```
inurl:/certs/server.key
```

```
inurl:print.htm intext:"Domain Name:" + "Open printable report"
```

```
"-- Dumped from database version" + "-- Dumped by pg_dump version" ext:txt | ext:sql | ext:env | ext:log	
```

```
/etc/config + "index of /" /
```

```
/etc/certs   "index of /" */*
```

```
intitle:"index of" inurl:admin/download
```

```
intitle:"index of" "dump.sql"
```

```
intitle:"index of" "*.cert.pem" | "*.key.pem"
```

```
"index of" inurl:database ext:sql | xls | xml | json | csv
```

```
ssh_host_dsa_key.pub + ssh_host_key + ssh_config = "index of / "
```

```
"-- Dumping data for table `admin`" | "-- INSERT INTO `admin`" "VALUES" ext:sql | ext:txt | ext:log | ext:env
```

```
intitle:index of .git/hooks/
```

```
inurl: /.git
```

```
intitle:"index of" "server.crt" | "server.csr"
```

```
"index of" "mysql.sh"
```

```
intitle:"index of" "slapd.conf"
```

```
intitle:"index of" "/system.log" | "/system.logs"
```

```
intitle:"index of" "/CFIDE/" intext:"administrator"
```

```
"-- Dumping data for table `users` | `people` | `member`" ext:sql | ext:txt | ext:log | ext:env
```

```
"-- Dumping data for table * " ext:sql | ext:xls intext:db | intext:database | intext:password | username	
```

```
intitle:"index of" "/app.log" | "/app.logs"
```

```
GitLab ssh.log ext:log
```

```
"index of" "users.ibd"
```

```
"-- PostgreSQL database dump complete" ext:sql | ext:txt | ext:log | ext:env
```

```
"ws_ftp.log" ext:log
```

```
"-- Dump completed" ext:sql | ext:txt | ext:log
```

```
intitle:"index of" "firewall.log" | "firewall.logs"
```

```
intitle:"index of" "/000~ROOT~000/"
```

```
"Share Link" inurl:/share.cgi?ssid=
```

```
intitle:"index of" /lsass.exe
```

```
intitle:"index of" /var/logs filetype:'"log | txt | csv"
```

```
Index: /wp-includes/Text/Diff
```

```
intitle:"Index of /" +.htaccess.old
```

```
intitle:"index of" "/root/etc/security/"
```

```
intitle:"index of" "app.log"
```

```
intitle:"Index of c:xampp"
```

```
"Index of" "/monitoring"
```

```
intitle:"index of" "/home/ROOT_PATH/"
```

```
intitle:"index of" "ssh_host_ecdsa_key"
```

```
Index of: /services/pancard/
```

```
intitle:"index of" "oauth-private.key"
```

```
intitle:"index of" "admin/sql/"
```

```
"Index of" "sass-cache"
```

```
intitle:"index of" "survey.cgi"
```

```
index of logs.tar
```

```
intitle:"index of" "uploads.old"
```

```
intitle:"index of" "api/admin"
```

```
intitle:"index of" inurl:ftp intext:admin
```

```
allintitle: sensitive ext:doc OR ext:xls OR ext:xlsx
```

```
intitle:"index of" "admin/config"
```

```
intitle:"index of" "system/config"
```

```
"index of" "/config/sql"
```

```
intitle:"index of" "/admin/backup"
```

```
intitle:"index of" "/admin_backup"
```

```
intitle:"index of" db.frm
```

```
intitle:"index of" "/db_backups/"
```

```
intitle:"index of" "proxy.pac" OR "proxy.pac.bak"
```

```
intitle:"index of" "common.crt" OR "ca.crt"
```

```
intitle:"index of" "global.asa"
```

```
intitle:"index of" "owncloud/config/*"
```

```
intitle: "index of" "MySQL-Router"
```

```
intitle:"index of" "iredadmin/*"
```

```
intitle:"index of" "cctv"
```

```
intitle:"index of" "/concrete/Authentication"
```

```
intitle:"index of" "maven-metadata.xml" "Port 80"
```

```
intitle:"index of" "jwt-auth"
```

```
intitle:"index of" "ftp.log"
```

```
intitle:"index of" "sms.log"
```

```
inurl:"/includes/OAuth2" intext:"index of /"
```

```
intitle:"index of" "config.py"
```

```
intitle:index.of "db.zip"
```

```
-pool intitle:"index of" wget-log -pub
```

```
intitle:"index of" "/Cloudflare-CPanel-7.0.1"
```

```
intitle:"index of" domain.key -public
```

```
intitle:"index of" api_key OR "api key" OR apiKey -pool
```

```
intitle:"index of" .oracle_jre_usage/
```

```
"key" OR key.jar intitle:"index of" webstart
```

```
index of /storage/logs/
```

```
intitle:index.of "chroot.conf"
```

```
intitle:index of "uploads"
```

```
intitle:"index of" "ws_ftp.log"
```

```
intitle:index.of "htaccess.txt"
```

```
intext:"index of" intext:..bak intext:config
```

```
site:* index.of: /android/manifest.xml
```

```
intitle:index.of "system.db"
```

```
intitle:index.of "database.db"
```

```
site:*/logs/default.htm
```

```
intitle:"index of" "/etc/mysql/"
```

```
intitle:index.of "admin" filetype:sql
```

```
site:ftp.* index of /ftp/backup
```

```
inurl:/wp-admin/includes/plugin-install.php
```

```
inurl:/wp-content/uploads/ninja-forms/ intitle:"index of"
```

```
site:*/logs/default.htm
```

```
intitle:index.of "admin.db"
```

```
indexof:backup/mysql
```
