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

# Registro de sistema

Los registros del sistema en Linux son archivos que registran eventos e información sobre el sistema operativo y las aplicaciones que se ejecutan en él.&#x20;

En Linux, los registros se almacenan en el directorio `/var/log`. Los archivos de registro más comunes son:

* `syslog`: Este archivo registra una variedad de eventos del sistema, como inicio de sesión de usuarios, inicio de servicios y errores.
* `auth.log`: Este archivo registra los intentos de inicio de sesión, tanto exitosos como fallidos.
* `kern.log`: Este archivo registra los mensajes del kernel, como errores de hardware y errores de software.
* `dmesg`: Este archivo registra los mensajes del kernel durante el arranque del sistema.
* `messages`: Este archivo es una combinación de los archivos `syslog`, `auth.log` y `kern.log`.

Para ver los registros del sistema, puede utilizar el comando `tail`.Para ver las últimas 10 líneas del archivo `syslog`, puede ejecutar el siguiente comando:

```
tail -f /var/log/syslog
```

También puede utilizar el comando `grep` para buscar texto específico en los registros. Para buscar todos los mensajes de inicio de sesión fallidos, puede ejecutar el siguiente comando:

```
grep failed /var/log/auth.log
```

Para configurar los registros del sistema, puede editar el archivo `/etc/syslog.conf`. Este archivo contiene las reglas que determinan qué eventos se registran en cada archivo de registro.

