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

# Configuración de SSH

Cómo Instalar SSH en Linux

Lo primero que necesitamos hacer es instalar SSH. Hay paquetes de software separados disponibles dependiendo de si deseas instalar el paquete del cliente, el paquete del servidor o ambos. El paquete del Cliente OpenSSH te permitirá usar SSH para iniciar sesión o iniciar conexiones con sistemas remotos. El paquete del Servidor OpenSSH te permitirá configurar el servicio SSH y aceptar conexiones entrantes. No es necesario (ni recomendado) instalar este paquete si solo planeas usar SSH como cliente. El comando SSH generalmente está disponible por defecto en todas las distribuciones de Linux, pero si tu sistema no lo tiene, puedes usar el comando apropiado a continuación para instalar el paquete del cliente OpenSSH con el administrador de paquetes de tu sistema. El segundo comando en cada ejemplo a continuación instalará el paquete del servidor (omitir si no lo necesitas).

Para instalar el Cliente y Servidor OpenSSH en Ubuntu, Debian y Linux Mint:

```bash
bashCopy code$ sudo apt update
$ sudo apt install openssh-client
$ sudo apt install openssh-server
```

Para instalar el Cliente y Servidor OpenSSH en Fedora, CentOS, AlmaLinux y Red Hat:

```bash
bashCopy code$ sudo dnf install openssh
$ sudo dnf install openssh-server
```

Para instalar el Cliente y Servidor OpenSSH en Arch Linux y Manjaro:

```bash
bashCopy code$ sudo pacman -S openssh # todo en un paquete
```

Uso del Comando SSH Ahora que SSH está instalado, podemos usar el comando ssh para conectarnos a un servidor remoto e iniciar sesión. La sintaxis básica es la siguiente, donde el usuario es el nombre de usuario y linuxconfig.org es el servidor remoto. También puedes usar la dirección IP en lugar del nombre de host.

```bash
bashCopy code$ ssh user@linuxconfig.org
```

El puerto predeterminado para que SSH escuche es el 22. Si el sistema remoto está ejecutando el servicio SSH en algún puerto no predeterminado, puedes especificar ese puerto con la opción -p en tu comando. El siguiente ejemplo muestra cómo te conectarías a un sistema remoto que está ejecutando el servicio en el puerto 2210.

```bash
bashCopy code$ ssh -p 2210 user@linuxconfig.org
```

Tener SSH instalado también nos da acceso al comando scp. El comando scp en Linux se utiliza para copiar archivos y directorios hacia o desde un sistema remoto. Funciona de manera muy similar al comando cp, excepto que copia archivos hacia o desde otros sistemas que están en tu red local o en algún lugar de Internet. Veamos un ejemplo simple donde usamos el comando scp para copiar un archivo local llamado file.txt a un servidor remoto con el nombre de host linuxconfig.org.

```bash
bashCopy code$ scp file.txt user@linuxconfig:/path/to/dest
```

NOTA - ACCESO SIN CONTRASEÑA Si te cansa escribir tu contraseña cada vez, puedes autenticarte utilizando claves RSA en su lugar.

Cómo Configurar el Servidor SSH Para permitir que los usuarios inicien sesión en tu sistema a través de SSH, te mostraremos cómo controlar el servicio y permitir las conexiones a través de tu firewall en los pasos a continuación.

Para comenzar a aceptar conexiones entrantes de SSH, necesitamos iniciar el servicio SSH con el comando systemctl. Para iniciar o detener el servidor SSH:

```bash
bashCopy code$ sudo systemctl start sshd
```

Y

```bash
bashCopy code$ sudo systemctl stop sshd
```

Para habilitar (hacer que SSH se inicie automáticamente en el arranque del sistema) o deshabilitar el servidor SSH:

```bash
bashCopy code$ sudo systemctl enable ssh
```

O

```bash
bashCopy code$ sudo systemctl disable ssh
```

Verifica si el servidor SSH está en ejecución utilizando el comando systemctl status.

```bash
bashCopy code$ sudo systemctl status ssh
```

El estado del sshd indica que el servicio está actualmente en ejecución.

Para aceptar conexiones entrantes, también deberás permitir el servicio a través del firewall de tu sistema. Los comandos para hacer eso pueden diferir dependiendo de tu distribución de Linux. Usa los apropiados a continuación.

En Ubuntu y sistemas que usan ufw (firewall sin complicaciones):

```bash
bashCopy code$ sudo ufw allow ssh
```

En distribuciones basadas en RHEL o cualquier otra que use firewalld:

```bash
bashCopy code$ sudo firewall-cmd --zone=public --permanent --add-service=ssh
$ sudo firewall-cmd --reload
```

O si solo estás usando iptables y no hay interfaz gráfica de firewall:

```bash
bashCopy code$ sudo iptables -A INPUT -p tcp --dport ssh -j ACCEPT
```

Eso es todo. Si no hay un enrutador físico o firewall bloqueando las conexiones al servidor SSH, debería estar listo para aceptar conexiones entrantes.

Recomendaciones Adicionales para el Servidor SSH
