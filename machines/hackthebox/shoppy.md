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

### Servidor Web

Ahora tenemos que ir al sitio web y enumerar con fuff.

`http://shoppy.htb`.

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

Se descubrió dos URL interesantes `http://shoppy.htb/login y http://shoppy.htb/exports`

## Acceder

### Acceder como administrador

Ahora en la URL login.

Si usamos una comillas simple (') en el campo de nombre de usuario, recibimos un 504 Gateway Time-out. Tenemos nuestro primer mensaje de error.El mensaje de error muestra la URL http://shoppy.htb/login?error=WrongCredentialsProbemos diferentes cargas útiles en el formulario de inicio de sesión.La carga útil adecuada para eludir el mecanismo de inicio de sesión a través de BurpSuite.

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

username=admin'||'1==1//&password=admin

```

Después de iniciar sesión, somos redirigidos a `http://shoppy.htb/admin`

Desde esta página, podemos buscar usuarios. Podemos buscar al usuario admin y recibir la contraseña de esta cuenta de usuario. Hemos intentado descifrar esta contraseña, pero parece que no se puede descifrar. Después de completar la carga útil `'||'1==1//` en la barra de búsqueda, muestra todas las cuentas de usuario existentes en la base de datos.Intentemos descifrar la contraseña de la cuenta de usuario john.La contraseña encontrada es `remembermethisway.` Con esta contraseña se puede  intentar iniciar sesión a través de SSH con esta contraseña. Después de enumerar alrededor, encontramos un subdominio adicional `http://mattermost.shoppy.htb`.Después de mirar alrededor, encontramos las credenciales para la cuenta de usuario `jaeger` con la contraseña `Sh0ppyBest@pp!`

## SSH acceder como jaeger <a href="#ssh-access-as-jaeger" id="ssh-access-as-jaeger"></a>

Con el usuario y la contraseña encontrada antes podemos acceder a la maquina con SSH.

## Movimiento lateral

Esta cuenta de usuario tiene permiso para ejecutar /home/deploy/password-manager en nombre de la cuenta de usuario deploy.Después de ejecutar este programa, solicita una contraseña maestra. Como podemos ejecutar el programa, también podemos intentar leerlo.Parece que la contraseña es: Sample

## Escalada de privilegios

&#x20;Ahora tenemos las credenciales para la cuenta de usuario deploy. Podemos cambiar a esta cuenta de usuario y ejecutar linpeas.sh.

## Explotación de Docker

La cuenta de usuario deploy está en el grupo docker. A través de [GTFObins](https://gtfobins.github.io/gtfobins/docker/) podemos encontrar la ruta a la escalada de privilegios.
