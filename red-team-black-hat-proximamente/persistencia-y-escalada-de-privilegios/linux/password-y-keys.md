# Password y Keys

## History Files

Si un usuario escribe accidentalmente su contraseña en la línea de comandos en lugar de en un prompt de contraseña, esta puede quedar registrada en un archivo de historial.

Visualiza el contenido de todos los archivos de historial ocultos en el directorio principal del usuario:

```bash
cat ~/.*history | less
```

Observa que el usuario ha intentado conectarse a un servidor MySQL en algún momento, usando el nombre de usuario "root" y una contraseña proporcionada a través de la línea de comandos. ¡Observa que no hay espacio entre la opción -p y la contraseña!

## Config Files

Los archivos de configuración a menudo contienen contraseñas en texto plano u otros formatos reversibles.

Enumera el contenido del directorio principal del usuario:

```bash
ls /home/user
```

Observa la presencia de un archivo de configuración llamado myvpn.ovpn. Visualiza el contenido del archivo:

```bash
cat /home/user/myvpn.ovpn
```

El archivo debería contener una referencia a otro lugar donde se pueden encontrar las credenciales del usuario root. Cambia al usuario root, utilizando las credenciales:

```bash
su root
```



## SSH Key



A veces, los usuarios hacen copias de seguridad de archivos importantes pero no los aseguran con los permisos correctos.

Busca archivos y directorios ocultos en el directorio raíz del sistema:

```bash
ls -la /
```

Observa que parece haber un directorio oculto llamado .ssh. Visualiza el contenido del directorio:

```bash
ls -l /.ssh
```

Nota que hay un archivo legible por todos llamado root\_key. Una inspección adicional de este archivo debería indicar que es una clave SSH privada. El nombre del archivo sugiere que es para el usuario root.

Copia la clave a tu máquina Kali (es más fácil simplemente ver el contenido del archivo root\_key y copiar/pegar la clave) y dale los permisos correctos, de lo contrario, tu cliente SSH se negará a usarla:

```bash
chmod 600 root_key
```

Usa la clave para iniciar sesión en la VM de Debian como la cuenta root (ten en cuenta que debido a la antigüedad de la máquina, se requieren algunos ajustes adicionales al usar SSH):

```bash
su root
```

```bash
ssh -i root_key -oPubkeyAcceptedKeyTypes=+ssh-rsa -oHostKeyAlgorithms=+ssh-rsa root@DIRECCION_IP_DE_LA_MAQUINA
```
