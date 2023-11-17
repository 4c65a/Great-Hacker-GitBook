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

# Configurar servidor web apache

### Introducción

El servidor web Apache HTTP es el servidor web más utilizado en todo el mundo. Ofrece características poderosas, como módulos dinámicamente cargables, sólido soporte multimedia y una integración extensa con otro software popular. En esta guía, explicaremos cómo instalar un servidor web Apache en tu servidor Ubuntu 20.04.

**Prerrequisitos:**

* Usuario regular, no root, con privilegios sudo.
* Firewall básico habilitado.

### Paso 1 — Instalar Apache

Apache está disponible en los repositorios de software predeterminados de Ubuntu. Para instalarlo, actualiza el índice de paquetes y luego instala el paquete `apache2`:

```bash
bashCopy codesudo apt update
sudo apt install apache2
```

### Paso 2 — Ajustar el Cortafuegos

Antes de probar Apache, ajusta la configuración del cortafuegos para permitir el acceso externo a los puertos web predeterminados. Lista los perfiles de aplicación disponibles en UFW:

```bash
bashCopy codesudo ufw app list
```

Permite el tráfico en el puerto 80:

```bash
bashCopy codesudo ufw allow 'Apache'
```

Verifica el cambio:

```bash
bashCopy codesudo ufw status
```

### Paso 3 — Verificar el Servidor Web

Después de la instalación, Apache se inicia automáticamente. Verifica el estado del servicio:

```bash
bashCopy codesudo systemctl status apache2
```

Accede a la página de inicio predeterminada de Apache a través de tu dirección IP:

```bash
bashCopy codehostname -I
```

O usa la herramienta Icanhazip:

```bash
bashCopy codecurl -4 icanhazip.com
```

Ingresa la IP en tu navegador:

```arduino
arduinoCopy codehttp://tu_direccion_ip
```

Deberías ver la página predeterminada de Apache.

### Paso 4 — Administrar el Proceso de Apache

Administra el servicio Apache con systemctl:

* Detener: `sudo systemctl stop apache2`
* Iniciar: `sudo systemctl start apache2`
* Reiniciar: `sudo systemctl restart apache2`
* Recargar: `sudo systemctl reload apache2`
* Deshabilitar inicio automático: `sudo systemctl disable apache2`
* Habilitar inicio automático: `sudo systemctl enable apache2`

### Paso 5 — Configurar Virtual Hosts (Recomendado)

Usa hosts virtuales para alojar varios dominios. Crea una estructura de directorios para tu dominio:

```bash
bashCopy codesudo mkdir /var/www/tu_dominio
sudo chown -R $USER:$USER /var/www/tu_dominio
sudo chmod -R 755 /var/www/tu_dominio
```

Crea un index.html de ejemplo:

```bash
bashCopy codesudo nano /var/www/tu_dominio/index.html
```

Agrega contenido HTML de ejemplo. Crea un archivo de host virtual:

```bash
bashCopy codesudo nano /etc/apache2/sites-available/tu_dominio.conf
```

Pega el bloque de configuración, actualiza las rutas y guarda.

Habilita el host virtual:

```bash
bashCopy codesudo a2ensite tu_dominio.conf
sudo a2dissite 000-default.conf
sudo apache2ctl configtest
sudo systemctl restart apache2
```

Accede a tu dominio en el navegador.

### Paso 6 – Conocer Archivos y Directorios Importantes de Apache

Explora directorios y archivos importantes:

* **Contenido:** `/var/www/html`
* **Configuración del Servidor:** `/etc/apache2`
* **Registros del Servidor:** `/var/log/apache2/access.log` y `/var/log/apache2/error.log`

\
