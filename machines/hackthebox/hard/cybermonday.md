---
description: >-
  SSRF using CRLF injection, Lateral movement, API, LFI, privilege escalation,
  docker.
---

# Cybermonday

```
IP = 10.10.11.228 
```

## HOST

```
10.10.11.228 cybermonday.htb
```

## Reconocimiento

<figure><img src="../../../.gitbook/assets/Inicio.png" alt=""><figcaption></figcaption></figure>

### NMAP

```
sudo nmap -sS -p- -Pn --open 10.10.11.228 -vvv -oG PORT.txt
[sudo] password for titan:
Starting Nmap 7.94 ( https://nmap.org ) at 2023-12-10 21:52 UTC
Initiating SYN Stealth Scan at 21:52
Scanning cybermonday.htb (10.10.11.228) [65535 ports]
Discovered open port 22/tcp on 10.10.11.228
Discovered open port 80/tcp on 10.10.11.228
SYN Stealth Scan Timing: About 41.98% done; ETC: 21:53 (0:00:43 remaining)
Completed SYN Stealth Scan at 21:54, 86.17s elapsed (65535 total ports)
Nmap scan report for cybermonday.htb (10.10.11.228)
Host is up, received user-set (0.41s latency).
Scanned at 2023-12-10 21:52:35 UTC for 87s
Not shown: 64514 closed tcp ports (reset), 1019 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack ttl 63
80/tcp open  http    syn-ack ttl 62

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 86.26 seconds
           Raw packets sent: 85490 (3.762MB) | Rcvd: 78122 (3.215MB)
```

**Servicios**

```
nmap -sV -p 80,22  10.10.11.228
Starting Nmap 7.94 ( https://nmap.org ) at 2023-12-10 22:05 UTC
Nmap scan report for cybermonday.htb (10.10.11.228)
Host is up (0.22s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
80/tcp open  http    nginx 1.25.1
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.99 seconds
```

**Whatweb**

```
whatweb http://cybermonday.htb/
http://cybermonday.htb/ [200 OK] Cookies[XSRF-TOKEN,cybermonday_session], Country[RESERVED][ZZ]
, HTML5, HTTPServer[nginx/1.25.1], HttpOnly[cybermonday_session], IP[10.10.11.228], PHP[8.1.20]
, Script, Title[Welcome - Cyber Monday], X-Powered-By[PHP/8.1.20], X-UA-Compatible[IE=edge], ng
inx[1.25.1]
```

## Enumeracion de directorios

```
feroxbuster --url http://cybermonday.htb -w ~/.repositories/SecLists/Discovery/Web-Content/co
mmon.txt --filter-status 400 401 402 403 404

 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.7.1
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://cybermonday.htb
 🚀  Threads               │ 50
 📖  Wordlist              │ /home/titan/.repositories/SecLists/Discovery/Web-Content/common.tx
t
 💢  Status Code Filters   │ [400, 401, 402, 403, 404]
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.7.1
 🏁  HTTP methods          │ [GET]
 🔃  Recursion Depth       │ 4
 🎉  New Version Available │ https://github.com/epi052/feroxbuster/releases/latest
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
200      GET       21l       56w      603c http://cybermonday.htb/.htaccess
200      GET      239l      986w        0c http://cybermonday.htb/
301      GET        7l       11w      169c http://cybermonday.htb/assets => http://cybermonday.
htb/assets/
301      GET        7l       11w      169c http://cybermonday.htb/assets/css => http://cybermon
day.htb/assets/css/
301      GET        7l       11w      169c http://cybermonday.htb/assets/img => http://cybermon
day.htb/assets/img/
301      GET        7l       11w      169c http://cybermonday.htb/assets/js => http://cybermond
ay.htb/assets/js/
301      GET        7l       11w      169c http://cybermonday.htb/assets/views => http://cyberm
onday.htb/assets/views/
301      GET        7l       11w      169c http://cybermonday.htb/assets/views/components => ht
tp://cybermonday.htb/assets/views/components/
```

## Busqueda de vulnerabilidades y explotacion

**Registros**

```
Username: kirov
password : admin
email: kirov@htb.com
```

