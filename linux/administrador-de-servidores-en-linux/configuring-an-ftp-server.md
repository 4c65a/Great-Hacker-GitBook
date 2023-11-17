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
    sudo systemctl restart vsftpd
    ```

### Crear un usuario FTP

1.  Para crear una nueva cuenta.

    ```bash
    sudo useradd -m user
    sudo passwd user
    ```
2.  Para verificar que todo funciona correctamente, debe almacenar al menos un archivo en el directorio de inicio de ftpuser. Este archivo debería estar visible cuando iniciemos sesión en FTP en los siguientes pasos.

    ```bash
    sudo bash -c "echo FTP TESTING > /home/ftpuser/FTP-TEST"
    ```

### Conéctese al servidor FTP a través de la línea de comando

1.  Conectarse a su servidor FTP.

    ```
    ftp 127.0.0.1
    ```

### Permitir acceso anónimo en vsftpd

1.  Primero, necesitaremos editar el `/etc/vsftpd.conf`archivo.

    ```
    sudo nvim /etc/vsftpd.conf
    ```
2.  A continuación, busque la `anonymous_enable=NO`línea y cambie la configuración a `YES`.

    ```
    anonymous_enable=YES
    ```
3.  Cuando termine, salga de este archivo mientras guarda los nuevos cambios, luego reinicie el servicio vsftpd para que los cambios surtan efecto.

    ```
    sudo systemctl restart vsftpd
    ```

    ***

    ***
4.  Para probar el inicio de sesión anónimo, emita el `ftp 127.0.0.1`comando, utilícelo `anonymous`como nombre de usuario y una contraseña en blanco. Debería recibir un `230 Login successful.`



\
