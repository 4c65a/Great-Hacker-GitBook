# Password y Keys

## History Files

Si un usuario escribe accidentalmente su contraseña en la línea de comandos en lugar de en un prompt de contraseña, esta puede quedar registrada en un archivo de historial.

Visualiza el contenido de todos los archivos de historial ocultos en el directorio principal del usuario:

```bash
cat ~/.*history | less
```

## Config Files

Los archivos de configuración a menudo contienen contraseñas en texto plano u otros formatos reversibles.

## SSH Key

A veces, los usuarios hacen copias de seguridad de archivos importantes pero no los aseguran con los permisos correctos.

Busca archivos y directorios ocultos en el directorio raíz del sistema:

```bash
ls -la /
```

Observa que parece haber un directorio oculto llamado .ssh.

```bash
ls -l /.ssh
```
