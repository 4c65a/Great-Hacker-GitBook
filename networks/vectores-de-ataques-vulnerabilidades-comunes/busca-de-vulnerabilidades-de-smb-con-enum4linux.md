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

# Busca de vulnerabilidades de SMB con enum4linux

## Buscar los servidores con nmap

TCP 135           RPC

TCP 139           NetBIOS Session

TCP 389           LDAP Server

TCP 445           SMB File Service

TCP 9389          Active Directory Web Services

TCP/UDP 137   NetBIOS Name Service

UDP 138           NetBIOS Datagram

Para buscar los servicios disponibles en los hosts de la red virtual.

```
nmap -sN 192.215.26.11
```

### Enum4linux para enumerar usuarios y recursos compartidos de archivos de red

**Las opciones más comunes son:**

`-U encuentra usuarios configurados`

`-S obtiene una lista de archivos compartidos`

`-G obtener una lista de los grupos y sus miembros.`

`-P enumera las políticas de contraseña`

`-i obtener una lista de impresoras`

**Buscar los usuarios configurados**

```
enum4linux -U 192.215.26.11
```

**Enumere los recursos compartidos de archivos disponibles**

```
enum4linux -Sv 192.215.26.11
```

**Utilice el comando enum4linux -P para enumerar las políticas de contraseña**

```
enum4linux -P 192.215.26.11
```

**Utilice el comando enum4linux -a para realizar un escaneo en el posible destino del servidor Samba**&#x20;

```
enum4linux -a 192.215.26.11
```

### Smbclient para transferir archivos entre sistemas

```bash
# Crear un archivo de texto llamado badfile.txt
cat >> badfile.txt
Este es un archivo malo.
Presione CTRL-C para escribir el archivo.

# Ver opciones disponibles de smbclient
smbclient --help

# Enumerar recursos compartidos en el host de destino
smbclient -L //172.17.0.2/
Contraseña para [GRUPO DE TRABAJO\kali]: <Presione enter>

# Conectarse al recurso compartido tmp
smbclient //172.17.0.2/tmp
Contraseña para [GRUPO DE TRABAJO\kali]: <Presione enter>

# Escribir "ayuda" para ver comandos disponibles
help

# Ver contenido del recurso compartido
dir

# Subir el archivo badfile.txt al servidor de destino 
put badfile.txt 

# Verificar que el archivo se haya cargado correctamente
dir

# Salir de smbclient
quit
```
