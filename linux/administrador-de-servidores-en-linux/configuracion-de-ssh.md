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

## Instalar SSH en Linux

```bash
sudo apt install openssh-client
sudo apt install openssh-server
```

```bash
sudo pacman -S openssh
```

Uso del Comando SSH Ahora que SSH está instalado, podemos usar el comando ssh para conectarnos a un servidor remoto e iniciar sesión. La sintaxis básica es la siguiente, donde el usuario es el nombre de usuario y linuxconfig.org es el servidor remoto. También puedes usar la dirección IP en lugar del nombre de host.

```bash
ssh user@linuxconfig.org
```

El puerto predeterminado para que SSH escuche es el 22.

```bash
ssh -p 22 user@linuxconfig.org
```

Tener SSH instalado también nos da acceso al comando scp. El comando scp en Linux se utiliza para copiar archivos y directorios hacia o desde un sistema remoto. Funciona de manera muy similar al comando cp, excepto que copia archivos hacia o desde otros sistemas que están en tu red local o en algún lugar de Internet. Veamos un ejemplo simple donde usamos el comando scp para copiar un archivo local llamado file.txt a un servidor remoto con el nombre de host linuxconfig.org.

```bash
scp file.txt user@linuxconfig:/path/to/dest
```

Para comenzar a aceptar conexiones entrantes de SSH, necesitamos iniciar el servicio SSH con el comando systemctl. Para iniciar o detener el servidor SSH:

```bash
sudo systemctl start sshd
```

Y

```bash
sudo systemctl stop sshd
```

Para habilitar (hacer que SSH se inicie automáticamente en el arranque del sistema) o deshabilitar el servidor SSH:

```bash
sudo systemctl enable ssh
```

O

```bash
sudo systemctl disable ssh
```

Verifica si el servidor SSH está en ejecución utilizando el comando systemctl status.

```bash
sudo systemctl status ssh
```

En Ubuntu y sistemas que usan ufw (firewall sin complicaciones):

```bash
sudo ufw allow ssh
```

O si solo estás usando iptables y no hay interfaz gráfica de firewall:

```bash
sudo iptables -A INPUT -p tcp --dport ssh -j ACCEPT
```
