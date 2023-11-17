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

# Configuring an FTP Server

### Cómo instalar vsftpd en Linux

```bash
sudo apt install vsftpd
```

```bash
sudo pacman -S vsftpd
```

### Configurar un servidor vsftpd

* Cambiemos el nombre del archivo de configuración predeterminado

```bash
sudo mv /etc/vsftpd.conf /etc/vsftpd.conf_orig
```

* Cree un nuevo archivo de configuración vsftpd usando nano o el editor de texto que prefiera:

```bash
sudo nvim /etc/vsftpd.conf
```

1.  Esta configuración  para un servidor FTP básico:

    ```bash
    listen=NO
    listen_ipv6=YES
    anonymous_enable=NO
    local_enable=YES
    write_enable=YES
    local_umask=022
    dirmessage_enable=YES
    use_localtime=YES
    xferlog_enable=YES
    connect_from_port_20=YES
    chroot_local_user=YES
    secure_chroot_dir=/var/run/vsftpd/empty
    pam_service_name=vsftpd
    rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
    rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
    ssl_enable=NO
    pasv_enable=Yes
    pasv_min_port=10000
    pasv_max_port=10100
    allow_writeable_chroot=YES
    ```


2.  Permitir el tráfico de FTP:

    En Ubuntu y sistemas que utilizan ufw (firewall sencillo):

    ```bash
    sudo ufw  20,21 proto tcp
    ```

    O si sólo estás usando iptables y no tienes una interfaz de firewall:

    ```bash
    sudo iptables -A INPUT -m state --state NEW,ESTABLISHED -m tcp -p tcp --dport 20,21 -j ACCEPT
    ```
3.  Con el archivo de configuración guardado y las reglas del firewall actualizadas, reinicie vsftpd para aplicar los nuevos cambios:

    ```
    $ sudo systemctl reiniciar vsftpd
    ```

### Crear un usuario FTP

Nuestro servidor FTP está listo para recibir conexiones entrantes, por lo que ahora es el momento de crear una nueva cuenta de usuario que usaremos para conectarnos al servicio FTP.

1.  Utilice este primer comando para crear una nueva cuenta llamada `ftpuser`y el segundo comando para establecer una contraseña para la cuenta:

    ```
    $ sudo useradd -m ftpuser
    $ sudo contraseña ftpuser
    Nueva contraseña:
    Reescriba nueva contraseña:
    passwd: contraseña actualizada correctamente
    ```
2.  Para verificar que todo funciona correctamente, debe almacenar al menos un archivo en el directorio de inicio de ftpuser. Este archivo debería estar visible cuando iniciemos sesión en FTP en los siguientes pasos.

    ```
    $ sudo bash -c "echo PRUEBA DE FTP > /home/ftpuser/FTP-TEST"
    ```

### Conéctese al servidor FTP a través de la línea de comando

1.  Ahora debería poder conectarse a su servidor FTP ya sea por dirección IP o nombre de host. Para conectarse desde la línea de comando y verificar que todo esté funcionando, abra una terminal y use el `ftp`comando para conectarse a su dirección de loopback (127.0.0.1).

    ```
    $ ftp 127.0.0.1
    ```


2.  Como puede ver en la captura de pantalla anterior, pudimos iniciar sesión en el servidor FTP especificando el nombre de usuario y la contraseña que configuramos anteriormente. A continuación, intentemos emitir un `ls`comando, que debería enumerar el archivo de prueba que creamos en los pasos anteriores.

    ```
    ftp>ls
    ```



***

***

\
Su resultado debería verse como la captura de pantalla anterior, indicando un inicio de sesión exitoso y un `ls`comando que revela nuestro archivo de prueba que creamos anteriormente.

### Conéctese al servidor FTP a través de GUI

La mayoría de los entornos de escritorio tienen una forma integrada de conectarse a servidores FTP. Incluso si el suyo no lo hace, hay muchos clientes FTP gratuitos disponibles para Linux. En las instrucciones a continuación, usaremos el entorno de escritorio GNOME en Ubuntu para conectarnos al servidor FTP. Si está ejecutando otra GUI, busque una opción para conectarse a un servidor externo en su [administrador de archivos](https://linuxconfig.org/best-file-manager-for-linux) ; desde allí, las instrucciones deberían ser más o menos las mismas que se muestran a continuación:

1.  En su administrador de archivos, haga clic en "Otras ubicaciones" (puede llamarse de otra manera si no usa GNOME) e ingrese `ftp://127.0.0.1`en el cuadro "Conectar al servidor" en la parte inferior de la ventana y haga clic en conectar.


2.  Elija "usuario registrado" y luego ingrese las credenciales de la cuenta FTP que configuramos anteriormente y haga clic en conectar.


3.  Tras una conexión exitosa, verá el archivo de prueba que creó anteriormente. Ahora podrá descargar y ver este archivo, o cargar su propio contenido en el directorio.



### Permitir acceso anónimo en vsftpd

Hasta ahora hemos visto cómo crear nuevos usuarios que puedan acceder al servidor FTP. Si desea que otros puedan acceder a su servidor FTP sin proporcionar un nombre de usuario y contraseña, puede configurar la autenticación anónima. Siga los pasos a continuación para configurarlo.

1.  Primero, necesitaremos editar el `/etc/vsftpd.conf`archivo, así que ábrelo con nano o cualquier otro editor de texto.

    ```
    $ sudo nano /etc/vsftpd.conf
    ```
2.  A continuación, busque la `anonymous_enable=NO`línea y cambie la configuración a `YES`.

    ```
    anónimo_enable=SÍ
    ```
3.  Cuando termine, salga de este archivo mientras guarda los nuevos cambios, luego reinicie el servicio vsftpd para que los cambios surtan efecto.

    ```
    $ sudo systemctl reiniciar vsftpd
    ```

    ***

    ***
4.  Para probar el inicio de sesión anónimo, emita el `ftp 127.0.0.1`comando, utilícelo `anonymous`como nombre de usuario y una contraseña en blanco. Debería recibir un `230 Login successful`mensaje como se muestra en la captura de pantalla a continuación.



### Cambiar el número de puerto FTP predeterminado

De forma predeterminada, el protocolo FTP escucha en el puerto 21 para la autenticación del usuario y en el puerto 20 para la transferencia de datos. Sin embargo, podemos cambiar este comportamiento realizando una pequeña edición en el `/etc/vsftpd.conf`archivo. En la parte inferior del archivo, use la `listen_port`directiva para especificar un puerto diferente para que lo use vsftpd. Por ejemplo, agregar la siguiente línea le indicará a vsftpd que escuche en el puerto 2121:

```
puerto_escucha=2121
```

\
