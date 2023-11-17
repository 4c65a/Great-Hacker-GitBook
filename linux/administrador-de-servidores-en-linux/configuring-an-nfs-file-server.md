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

# Configuring an NFS File Server

## Configuración del Servidor NFS

```bash
sudo apt install nfs-kernel-server
```

A continuación, asegúrate de que el servicio NFS esté en ejecución y se inicie automáticamente en los arranques.

```bash
sudo systemctl enable --now nfs-server
```

Crear un directorio ,para almacenaremos nuestra compartición NFS en /media/nfs.

```bash
sudo mkdir -p /media/nfs
```

Luego, editaremos el archivo de configuración /etc/exports. Aquí puedes configurar qué directorios estás compartiendo y quién puede acceder a ellos.

```bash
sudo nano /etc/exports
```

En el archivo, cada compartición tiene su propia línea. Esa línea comienza con la ubicación de la compartición en la máquina del servidor. Frente a eso, puedes listar el nombre de host de un cliente aceptado, si está disponible en el archivo de hosts del servidor, o una IP o rango de IPs. Directamente detrás de la dirección IP, coloca las reglas para la compartición entre paréntesis. En conjunto, debería lucir algo así:

```bash
/media/nfs		192.168.1.0/24(rw,sync,no_subtree_check)
```

Una vez que hayas configurado todo según tus preferencias, guarda y cierra el archivo. Luego, ejecuta el comando exportfs para cargar tu nueva configuración de exportaciones.

```bash
sudo exportfs -arv
```

Conexión al Servidor NFS desde Máquina(s) Cliente

Esta sección de la guía mostrará cómo utilizar una máquina cliente para conectarte a la compartición NFS que configuramos en la sección anterior.

Lo primero que debemos hacer es instalar los paquetes NFS adecuados en nuestro sistema. Utiliza el comando apropiado a continuación para instalarlo con el administrador de paquetes de tu sistema.

En Ubuntu, Linux Mint y otras distribuciones basadas en Debian:

```bash
sudo apt install nfs-common
```

Con el paquete instalado, podrás montar la(s) compartición(es) NFS. Para probarlo, elige un directorio para montar y ejecuta el comando mount con privilegios de root para montar la compartición en red. Estamos especificando la IP del servidor NFS en este comando, que resulta ser 192.168.1.110.

```bash
sudo mount -t nfs4 192.168.1.110:/media/nfs /media/share
```

Para una solución más permanente, puedes agregar la compartición al archivo /etc/fstab de tu cliente. La sintaxis general se parece mucho al comando que acabas de usar para montar tu compartición. Comienza con la ubicación de la compartición en tu red. Sigue eso con dónde se montará la compartición. El tipo de sistema de archivos aquí es nfs4. Las opciones dependen de ti, pero usar los valores predeterminados y permitir el acceso de usuario son bastante comunes para comparticiones no sensibles. El resultado final debería parecerse un poco al ejemplo a continuación.

```bash
192.168.1.110:/media/nfs	/media/share	nfs4	defaults,user,exec	0 0
```

Si no estás seguro de si la compartición estará siempre disponible en el cliente, agrega noauto a la lista de opciones para evitar que tu sistema intente montarlo automáticamente.

```bash
192.168.1.110:/media/nfs	/media/share	nfs4	defaults,user,exec,noauto	0 0
```

Para ejecutar el fstab que acabas de editar, ejecuta el siguiente comando de montaje.

```bash
sudo mount -a
```

Tu compartición debería estar montada exactamente donde la especificaste.
