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

# Escaneo de puertos con nmap

**Nmap** (escrito por Gordon Lyon, también conocido como Fyodor) es uno de los escáneres de puertos más populares, versátiles y robustos disponibles. Se ha desarrollado activamente durante más de dos décadas y ofrece numerosas funciones más allá del escaneo de puertos.

**Algunos de los ejemplos de escaneo de Nmap que cubriremos en este módulo se ejecutan utilizando sudo. Esto se debe a que bastantes opciones de escaneo de Nmap requieren acceso a sockets raw,** que a su vez requieren privilegios de root. Los sockets raw permiten la manipulación quirúrgica de paquetes TCP y UDP. Sin acceso a sockets raw, Nmap está limitado, ya que recurre a la creación de paquetes utilizando la API estándar de sockets Berkeley.\*\*

**Antes de explorar algunos ejemplos de escaneo de puertos, debemos comprender la huella que cada escaneo de Nmap deja en la red y los hosts escaneados.**

**Un escaneo TCP predeterminado de Nmap escaneará los 1000 puertos más populares en una máquina determinada. Antes de comenzar a ejecutar escaneos a ciegas, examinemos la cantidad de tráfico enviado por este tipo de escaneo. Escanearemos una de las máquinas del laboratorio mientras monitoreamos la cantidad de tráfico enviado al host objetivo usando iptables.**

**Utilizaremos varias opciones de iptables. Primero, usemos la opción -I para insertar una nueva regla en una cadena determinada, que en este caso incluye tanto la cadena INPUT (entrada) como la OUTPUT (salida), seguida del número de regla. Podemos usar -s para especificar una dirección IP de origen, -d para especificar una dirección IP de destino y -j para ACCEPTAR el tráfico. Finalmente, usaremos la opción -Z para poner a cero los contadores de paquetes y bytes en todas las cadenas.**

```
kali@kali:~$ sudo iptables -I INPUT 1 -s 192.168.50.149 -j ACCEPT
kali@kali:~$ sudo iptables -I OUTPUT 1 -d 192.168.50.149 -j ACCEPT
kali@kali:~$ sudo iptables -Z
```

**Habiendo configurado nuestras reglas de iptables para el escaneo, generemos algo de tráfico usando nmap:**

```
kali@kali:~$ nmap 192.168.50.149
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-09 05:12 EST
Nmap scan report for 192.168.50.149
Host is up (0.10s latency).
Not shown: 989 closed tcp ports (conn-refused)
PORT      STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
Nmap done: 1 IP address (1 host up) scanned in 10.95 seconds
```

**El escaneo se completó y reveló algunos puertos abiertos.**

**Ahora revisemos algunas estadísticas de iptables para tener una idea más clara de cuánto tráfico generó nuestro escaneo. Podemos usar la opción `-v` para agregar verbosidad a nuestra salida, `-n` para habilitar la salida numérica y `-L` para listar las reglas presentes en todas las cadenas.**

```
kali@kali:~$ sudo iptables -vn -L
Chain INPUT (policy ACCEPT 1270 packets, 115K bytes)
pkts bytes target
prot opt in out source
1196 47972 ACCEPT all -- * * 192.168.50.149

Chain OUTPUT (policy ACCEPT 1264 packets, 143K bytes)
pkts bytes target
prot opt in out source destination
1218 72640 ACCEPT all -- * * 0.0.0.0/0 192.168.50.149
```

**Según la salida, este escaneo predeterminado de 1000 puertos generó alrededor de 72 KB de tráfico.**

**Usemos iptables -Z para poner a cero los contadores de paquetes y bytes en todas las cadenas nuevamente y ejecutemos otro escaneo de nmap, esta vez usando -p para especificar todos los puertos TCP.**

```
kali@kali:~$ sudo iptables -Z
kali@kali:~$ nmap -p 1-65535 192.168.50.149
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-09 05:23 EST
Nmap scan report for 192.168.50.149
```

**Como era de esperar, el escaneo de todos los puertos TCP generará mucho más tráfico.**

**Al comprender la cantidad de tráfico que genera un escaneo de puertos, podemos tomar decisiones más informadas sobre cuándo y cómo realizar un escaneo. Además, al monitorear el tráfico del escaneo, podemos identificar posibles anomalías que podrían indicar que el objetivo está detectando o bloqueando nuestros intentos de escaneo.**

**Habiendo configurado iptables, ejecutemos un escaneo de Nmap en un host local probando explícitamente todos los 65535 puertos TCP:**

```
kali@kali:~$ nmap -p 1-65535 192.168.50.149
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-09 05:23 EST
Nmap scan report for 192.168.50.149
Host is up (0.11s latency).
Not shown: 65510 closed tcp ports (conn-refused)
PORT    STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
47001/tcp open  winrm
49664/tcp open  unknown
...
Nmap done: 1 IP address (1 host up) scanned in 2141.22 seconds
```

**Como era de esperar, el escaneo de todos los puertos TCP genera considerablemente más tráfico:**

```
kali@kali:~$ sudo iptables -vn -L
Chain INPUT (policy ACCEPT 67996 packets, 6253K bytes)
pkts bytes target
prot opt in out source
68724 2749K ACCEPT all -- * * 192.168.50.149

Chain OUTPUT (policy ACCEPT 67923 packets, 7606K bytes)
pkts bytes target
prot opt in out source destination
68807 4127K ACCEPT all -- * * 0.0.0.0/0 192.168.50.149
```

**El escaneo completo del puerto local generó aproximadamente 4 MB de tráfico, una cantidad significativamente mayor que el escaneo predeterminado de 1000 puertos. Sin embargo, este escaneo completo ha descubierto más puertos que el escaneo TCP predeterminado.**

**Nuestros resultados implican que un escaneo completo de Nmap de una red de clase C (254 hosts) resultaría en el envío de más de 1000 MB de tráfico a la red. Idealmente, un escaneo completo de puertos TCP y UDP de cada máquina objetivo proporcionaría la información más precisa sobre los servicios de red expuestos. Sin embargo, claramente necesitamos equilibrar las restricciones de tráfico (como un enlace ascendente lento) con el descubrimiento de puertos y servicios abiertos adicionales a través de un escaneo más exhaustivo. Esto es especialmente cierto para redes más grandes, como una evaluación de red de clase A o B.**

**Existen escáneres de puertos modernos como MASSCAN y RustScan que, aunque son más rápidos que Nmap, generan una cantidad considerable de tráfico concurrente. Nmap, por otro lado, utiliza un enfoque más metódico y escalonado, lo que puede ser beneficioso para evitar la detección y la denegación de servicio.**

**En conclusión, la cantidad de tráfico generado por un escaneo de puertos variará según el tipo de escaneo realizado, la cantidad de puertos escaneados y el sistema operativo objetivo. Es importante comprender el impacto que un escaneo de puertos puede tener en la red antes de realizarlo.**\
Explorando las técnicas de escaneo de Nmap: SYN Scanning

**Habiendo aprendido sobre el uso básico de Nmap, ahora exploraremos algunas de las diversas técnicas de escaneo de Nmap, comenzando con el escaneo SYN/Stealth.**

El escaneo SYN, también conocido como "Stealth", es la técnica de escaneo de Nmap más popular. Ofrece muchos beneficios y, por lo tanto, es la opción de escaneo predeterminada cuando no se especifica ninguna opción en un comando de nmap y el usuario tiene los privilegios de sockets raw requeridos.

**¿Cómo funciona?**

El escaneo SYN es un método de escaneo de puertos TCP que implica enviar paquetes SYN a varios puertos en una máquina objetivo sin completar el protocolo de enlace TCP de tres vías. Si un puerto TCP está abierto, la máquina objetivo debería enviar un paquete SYN-ACK, informándonos de que el puerto está abierto. En este punto, el escáner de puertos no se molesta en enviar el ACK final para completar el protocolo de enlace.

**Ventajas:**

* **Más discreto:** Debido a que el protocolo de enlace no se completa, la información no se pasa a la capa de aplicación y, como resultado, no aparecerá en ningún registro de la aplicación.
* **Más rápido:** Un escaneo SYN es más rápido y eficiente porque se envían y reciben menos paquetes.

**Desventajas:**

* **No siempre es silencioso:** El término "stealth" se refiere al hecho de que, en el pasado, los firewalls no registraban las conexiones TCP incompletas. Sin embargo, este ya no es el caso con los firewalls modernos y, aunque el apodo de "stealth" se ha mantenido, puede ser engañoso.
* **Puede ser bloqueado por firewalls:** Algunos firewalls están configurados para detectar y bloquear los escaneos SYN.

**Ejemplo:**

```
kali@kali:~$ sudo nmap -sS 192.168.50.149
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-09 06:31 EST
Nmap scan report for 192.168.50.149
Host is up (0.11s latency).
Not shown: 989 closed tcp ports (reset)
PORT     STATE SERVICE
53/tcp  open  domain
88/tcp  open  kerberos-sec
135/tcp open  msrpc
139/tcp open  netbios-ssn
389/tcp open  ldap
445/tcp open  microsoft-ds
464/tcp open  kpasswd5
593/tcp open  http-rpc-epmap
636/tcp open  ldapssl
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl
...
```

**En el próximo capítulo, exploraremos el escaneo de conexión TCP de Nmap, que realiza una conexión TCP completa para determinar el estado de un puerto.**

\
