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

# DNS Enumeracion

El Sistema de Nombres de Dominio (DNS)246 es una base de datos distribuida responsable de traducir nombres de dominio fáciles de recordar para los usuarios en direcciones IP. Es uno de los sistemas más críticos de internet.

Esto se facilita mediante una estructura jerárquica dividida en varias zonas, comenzando por la zona raíz de nivel superior.

Cada dominio puede utilizar diferentes tipos de registros DNS. Algunos de los tipos de registros DNS más comunes son:

* **NS:** Los registros de servidor de nombres contienen el nombre de los servidores autorizados que alojan los registros DNS de un dominio.
* **A:** También conocido como registro de host, el "registro A" contiene la dirección IPv4 de un nombre de host (como [www.megacorpone.com](https://www.megacorpone.com/)).
* **AAAA:** También conocido como registro de host cuádruple A, el "registro AAAA" contiene la dirección IPv6 de un nombre de host (como [www.megacorpone.com](https://www.megacorpone.com/)).
* **MX:** Los registros de intercambio de correo electrónico contienen los nombres de los servidores responsables de manejar el correo electrónico del dominio. Un dominio puede contener varios registros MX.
* **PTR:** Los registros de puntero se utilizan en zonas de búsqueda inversa y pueden encontrar los registros asociados con una dirección IP.
* **CNAME:** Los registros de nombre canónico se utilizan para crear alias para otros registros de host.
* **TXT:** Los registros TXT pueden contener cualquier dato arbitrario y utilizarse para diversos fines, como la verificación de la propiedad del dominio.

Debido a la gran cantidad de información contenida en el DNS, suele ser un objetivo lucrativo para la recopilación activa de información.

Demostremos esto usando el comando `host` para encontrar la dirección IP de [www.megacorpone.com](https://www.megacorpone.com/).

```
kali@kali:~$ host www.megacorpone.com
www.megacorpone.com has address 149.56.244.87
```

El comando `host` busca por defecto un registro A, pero también podemos consultar otros campos, como registros MX o TXT, especificando el tipo de registro en nuestra consulta usando la opción `-t`.

```
kali@kali:~$ host -t mx megacorpone.com
megacorpone.com mail is handled by 10 fb.mail.gandi.net.
megacorpone.com mail is handled by 20 spool.mail.gandi.net.
megacorpone.com mail is handled by 50 mail.megacorpone.com.
megacorpone.com mail is handled by 60 mail2.megacorpone.com.
```

En este caso, primero ejecutamos el comando `host` para obtener solo los registros MX de megacorpone.com, lo que devolvió cuatro registros de servidores de correo diferentes. Cada servidor tiene una prioridad diferente (10, 20, 50, 60) y el servidor con el número de prioridad más bajo se usará primero para reenviar el correo dirigido al dominio megacorpone.com (fb.mail.gandi.net).

Luego, ejecutamos el comando `host` nuevamente para recuperar solo los registros TXT de megacorpone.com, que devolvió dos entradas.

```
kali@kali:~$ host -t txt megacorpone.com
megacorpone.com descriptive text "Try Harder"
megacorpone.com descriptive text "google-site-
verification=U7B_b0HNeBtY4qYGQZNsEYXfCJ32hMNV3GtC0wWq5pA"
```

Ahora que hemos recopilado algunos datos iniciales del dominio megacorpone.com, podemos continuar usando consultas DNS adicionales para descubrir más nombres de host y direcciones IP que pertenecen al mismo dominio.

Por ejemplo, sabemos que el dominio tiene un servidor web con el nombre de host "[www.megacorpone.com](https://www.megacorpone.com/)".

Ejecutemos `host` contra este nombre de host.

```
kali@kali:~$ host www.megacorpone.com
www.megacorpone.com has address 149.56.244.87
```

Ahora, determinemos si megacorpone.com tiene un servidor con el nombre de host "idontexist". Observaremos la diferencia entre las salidas de la consulta.

```
kali@kali:~$ host idontexist.megacorpone.com
Host idontexist.megacorpone.com not found: 3(NXDOMAIN)
```

En el Listado 41, consultamos un nombre de host válido y recibimos una respuesta de resolución de IP. Por el contrario, el Listado 42 devolvió un error (NXDOMAIN247) indicando que no existe un registro DNS público para ese nombre de host. Como ahora comprendemos cómo buscar nombres de host válidos, podemos automatizar nuestros esfuerzos.

Una vez aprendidos los conceptos básicos de enumeración de DNS, podemos desarrollar técnicas de fuerza bruta de DNS para acelerar nuestra investigación.

La fuerza bruta es una técnica de prueba y error que busca encontrar información válida, como directorios en un servidor web, combinaciones de nombre de usuario y contraseña o, en este caso, registros DNS válidos. Mediante el uso de una lista de palabras que contiene nombres de host comunes, podemos intentar adivinar registros DNS y verificar la respuesta de los nombres de host válidos.

En los ejemplos anteriores, utilizamos búsquedas directas, que solicitan la dirección IP de un nombre de host para consultar tanto un nombre de host válido como uno no válido. Si el host resuelve con éxito un nombre a una IP, esto podría ser una indicación de un servidor funcional.

```
kali@kali:~$ cat list.txt
www
ftp
mail
owa
proxy
router
no
```

Primero, creamos una lista de posibles nombres de host.

```
kali@kali:~$ for ip in $(cat list.txt); do host $ip.megacorpone.com; done
www.megacorpone.com has address 149.56.244.87
Host ftp.megacorpone.com not found: 3(NXDOMAIN)
mail.megacorpone.com has address 51.222.169.212
Host owa.megacorpone.com not found: 3(NXDOMAIN)
Host proxy.megacorpone.com not found: 3(NXDOMAIN)
router.megacorpone.com has address 51.222.169.214
```

A continuación, podemos usar una línea de comandos de Bash para intentar resolver cada nombre de host.

```
kali@kali:~$ for ip in $(cat list.txt); do host $ip.megacorpone.com; done
www.megacorpone.com has address 149.56.244.87
Host ftp.megacorpone.com not found: 3(NXDOMAIN)
mail.megacorpone.com has address 51.222.169.212
Host owa.megacorpone.com not found: 3(NXDOMAIN)
Host proxy.megacorpone.com not found: 3(NXDOMAIN)
router.megacorpone.com has address 51.222.169.214
```

Utilizando esta lista de palabras simplificada, descubrimos entradas para "www", "mail" y "router". Sin embargo, los nombres de host "ftp", "owa" y "proxy" no se encontraron. Existen listas de palabras mucho más completas como parte del proyecto SecLists.248 Estas listas de palabras se pueden instalar en el directorio /usr/share/seclists usando el comando sudo apt install seclists.

Con la excepción del registro www, nuestra enumeración de fuerza bruta hacia adelante de DNS reveló un conjunto de direcciones IP dispersas en el mismo rango aproximado (51.222.169.X). Si el administrador de DNS

Si el administrador de DNS de megacorpone.com configuró registros PTR249 para el dominio, podríamos escanear el rango aproximado con búsquedas inversas para solicitar el nombre de host de cada IP.

Usemos un bucle para escanear las direcciones IP 51.222.169.200 a 51.222.169.254. Filtraremos los resultados no válidos (usando grep -v) mostrando solo las entradas que no contienen "no encontrado".

```
kali@kali:~$ for ip in $(seq 200 254); do host 51.222.169.$ip; done | grep -v "not
found"
...
208.169.222.51.in-addr.arpa domain name pointer admin.megacorpone.com.
209.169.222.51.in-addr.arpa domain name pointer beta.megacorpone.com.
210.169.222.51.in-addr.arpa domain name pointer fs1.megacorpone.com.
211.169.222.51.in-addr.arpa domain name pointer intranet.megacorpone.com.
212.169.222.51.in-addr.arpa domain name pointer mail.megacorpone.com.
213.169.222.51.in-addr.arpa domain name pointer mail2.megacorpone.com.
214.169.222.51.in-addr.arpa domain name pointer router.megacorpone.com.
215.169.222.51.in-addr.arpa domain name pointer siem.megacorpone.com.
216.169.222.51.in-addr.arpa domain name pointer snmp.megacorpone.com.
217.169.222.51.in-addr.arpa domain name pointer syslog.megacorpone.com.
218.169.222.51.in-addr.arpa domain name pointer support.megacorpone.com.
219.169.222.51.in-addr.arpa domain name pointer test.megacorpone.com.
220.169.222.51.in-addr.arpa domain name pointer vpn.megacorpone.com.
...
```

Hemos logrado resolver con éxito una serie de direcciones IP a hosts válidos utilizando búsquedas inversas de DNS. Si estuviéramos realizando una evaluación, podríamos extrapolar aún más estos resultados y analizar "mail2", "router", etc., y realizar una búsqueda inversa de los resultados positivos. Este tipo de escaneos suelen ser cíclicos; ampliamos nuestra búsqueda en función de la información que recibimos en cada ronda.

Ahora que hemos desarrollado nuestras habilidades básicas de enumeración de DNS, exploremos cómo podemos automatizar el proceso utilizando algunas aplicaciones.

En Kali Linux existen varias herramientas que pueden automatizar la enumeración de DNS. Dos ejemplos notables son DNSRecon y DNSenum; exploremos sus capacidades.

DNSRecon250 es un script avanzado de enumeración de DNS escrito en Python. Ejecutemos dnsrecon contra megacorpone.com, usando la opción `-d` para especificar un nombre de dominio y `-t` para especificar el tipo de enumeración a realizar (en este caso, un escaneo estándar).

```
kali@kali:~$ dnsrecon -d megacorpone.com -t std
[*] std: Performing General Enumeration against: megacorpone.com...
[-] DNSSEC is not configured for megacorpone.com
[*]
SOA ns1.megacorpone.com 51.79.37.18
[*]
NS ns1.megacorpone.com 51.79.37.18
[*]
NS ns3.megacorpone.com 66.70.207.180
[*]
NS ns2.megacorpone.com 51.222.39.63
[*]
MX mail.megacorpone.com 51.222.169.212
[*]
MX spool.mail.gandi.net 217.70.178.1
[*]
MX fb.mail.gandi.net 217
```

**Basándonos en la salida anterior, hemos logrado realizar un análisis DNS exitoso en los principales tipos de registros del dominio megacorpone.com.**

**Ahora intentemos forzar la búsqueda de nombres de host adicionales utilizando el archivo list.txt que creamos previamente para búsquedas directas.**

```
kali@kali:~$ cat list.txt
www
ftp
mail
owa
proxy
router
```

**Para realizar nuestro intento de fuerza bruta, utilizaremos la opción `-d` para especificar un nombre de dominio, `-D` para especificar un nombre de archivo que contenga posibles cadenas de subdominio y `-t` para especificar el tipo de enumeración a realizar, en este caso `brt` para fuerza bruta.**

```
kali@kali:~$ dnsrecon -d megacorpone.com -D ~/list.txt -t brt
[*] Usando el archivo de diccionario: /home/kali/list.txt (proporcionado por el usuario)
[*] brt: Realizando fuerza bruta de host y subdominio contra megacorpone.com...
[+]
A www.megacorpone.com 149.56.244.87
[+]
A mail.megacorpone.com 51.222.169.212
[+]
A router.megacorpone.com 51.222.169.214
[+] Se encontraron 3 registros
```

**Nuestro intento de fuerza bruta ha finalizado y hemos logrado resolver algunos nombres de host.**

**DNSEnum es otra herramienta popular de enumeración de DNS que se puede utilizar para automatizar aún más la enumeración de DNS del dominio megacorpone.com. Podemos pasarle a la herramienta algunas opciones, pero para este ejemplo solo le pasaremos el parámetro del dominio objetivo:**

```
kali@kali:~$ dnsenum megacorpone.com
...
dnsenum VERSION:1.2.6
-----
megacorpone.com
-----
...
Fuerza bruta con /usr/share/dnsenum/dns.txt:
_______________________________________________
admin.megacorpone.com.
5
PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.
IN
A
51.222.169.208
```

**Como resultado de nuestra extensa enumeración de DNS, ahora hemos descubierto varios hosts previamente desconocidos.**

**Como se mencionó al inicio de este módulo, la recopilación de información tiene un patrón cíclico, por lo que necesitaremos realizar todas las demás tareas de enumeración pasiva y activa en este nuevo subconjunto de hosts para revelar cualquier nuevo detalle potencial.**

**Las herramientas de enumeración que se han cubierto son prácticas y directas, y debemos familiarizarnos con cada una antes de continuar.**

**Habiendo cubierto las herramientas de Kali, exploremos qué tipo de enumeración de DNS podemos realizar desde una perspectiva de Windows.**

**Aunque no se encuentra en la lista LOLBAS, `nslookup` es otra excelente utilidad para la enumeración de DNS de Windows y aún se utiliza durante escenarios de `Living off the Land`. Las aplicaciones que pueden proporcionar una ejecución de código no intencionada normalmente se enumeran en el proyecto LOLBAS.**

**Una vez conectados al cliente Windows 11, podemos ejecutar una consulta simple para resolver el registro A del host `mail.megacorptwo.com`.**

```
C:\Users\student>nslookup mail.megacorptwo.com
La solicitud de DNS ha expirado.
El tiempo de espera fue de 2 segundos.
Servidor: Desconocido
Dirección: 192.168.50.151
Nombre:
mail.megacorptwo.com
Dirección: 192.168.50.154
```

**En la salida anterior, consultamos al servidor DNS predeterminado (`192.168.50.151`) para resolver la dirección IP de `mail.megacorptwo.com`, a lo que el servidor DNS respondió con "192.168.50.154".**

**De manera similar al comando `host` de Linux, `nslookup` puede realizar consultas más granulares. Por ejemplo, podemos consultar un DNS determinado sobre un registro TXT que pertenece a un host específico.**

```
C:\Users\student>nslookup -type=TXT info.megacorptwo.com 192.168.50.151
Servidor: Desconocido
Dirección: 192.168.50.151
```

"saludos del cuerpo del registro TXT"

**En este ejemplo, estamos consultando específicamente el servidor DNS `192.168.50.151` para cualquier registro TXT relacionado con el host `info.megacorptwo.com`.**

**La utilidad `nslookup` es tan versátil como el comando `host` de Linux y las consultas también se pueden automatizar aún más a través de `PowerShell` o scripts de `Batch`.**
