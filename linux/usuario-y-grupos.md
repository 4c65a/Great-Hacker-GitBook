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

# Usuario y grupos

## Comandos de gestión de usuarios <a href="#comandos-de-gestion-de-usuarios" id="comandos-de-gestion-de-usuarios"></a>

* `useradd` – crea un usuario.
* `userdel` – borra un usuario.
* `usermod` – realiza modificaciones sobre los datos de `/etc/passwd`. Tiene una opción para cada uno de los campos, excepto el campo **GECOS**. Incluye opciones para (des)bloquear un usuario (`--lock` y `--unlock`).
* `chfn` – modifica la información _finger_ (**GECOS**).
* `chsh` – modifica la shell.
*   `id` – imprime información sobre el usuario y sus grupos. Ej:

    ```bash
    id -u   # Imprime el UID
    id -un  # Imprime el login
    ```
* `chage` – _change age_ visualiza y modifica todas las fechas de contraseña de `/etc/shadow`.

### Para establecer y cambiar una contraseña:

* `usermod -p PASSWORD USER` guarda el password indicado sin encriptar (habría que pasarle un hash del password). No conviene usar esta opción.
* `passwd USER` es el comando que se utiliza, que permite introducir un password con seguridad.

### Comandos de gestión de grupos <a href="#comandos-de-gestion-de-grupos" id="comandos-de-gestion-de-grupos"></a>

La suite _Shadow_ también incluye los comandos:

* `groupadd` – añade un nuevo grupo
* `groupdel` – borra un grupo
* `groupmod` – Modifica la información de `/etc/groups`
* `gpasswd` – Modifica el password del grupo, reflejado en `/etc/gshadow`

### Modificar grupos de usuarios <a href="#modificar-grupos-de-usuarios" id="modificar-grupos-de-usuarios"></a>

```bash
# Modificar el grupo primario
usermod -g GROUP USER
# Reemplazar el grupo secundario
usermod -G GROUP USER
# Añadir un grupo secundario al usuario
usermod -a -G GROUP USER
```

#### Modificaciones de permisos <a href="#modificaciones-de-permisos" id="modificaciones-de-permisos"></a>

Los permisos de un archivo o directorio se pueden modificar con el comando:

```bash
chmod 
```

**Modo relativo.** Se puede tratar uno de los campos de forma aislada sin tocar el resto de los permisos:

* Se indica primero a quién se va a cambiar el permiso (se pueden poner varios):
  * `u`: usuario
  * `g`: grupo
  * `o`: otros
  * `a`: `all`, equivalente a `ugo` (también se puede dejar en blanco)
* Tipo de operación:
  * `+`: añadir permisos
  * `-`: quitar permisos
* Permisos:
  * `r`: lectura
  * `w`: excritura
  * `x`: ejecución

Ejemplos:

```bash
chmod u+x fichero
chmod go-x fichero
chmod +x fichero
```

**Modo absoluto.** Se puede reemplazar la información completa de los permisos utilizando un número en base 8 (octal) de tres cifras. Los permisos coinciden con los del número en binario. Lo bueno de trabajar en octal es que cada caracter se puede trabajar de manera independiente.

Ejemplo de permiso `754`:

* `7` en binario es `111` ⇒ permisos de _usuario_: `rwx`
* `5` en binario es `101` ⇒ permisos de _grupo_: `r-x`
* `4` en binario es `100` ⇒ permisos de _otros_: `r--`

```bash
$ chmod 754 file
$ ls -l file
-rwxr-xr-- 1 usuario grupo  2048 Jan  6 13:03 file
```

#### Máscara `umask` <a href="#mascara-umask" id="mascara-umask"></a>

La máscara del sistema operativo define los permisos que se asignan por defecto a archivos y directorios en el momento de su creación.

El comando `umask` sin parámetros imprime el valor que tiene actualmente, y se puede manejar en modo simbólico y modo octal:

```bash
umask
0022
umask -S
u=rwx,g=rx,o=rx
```

Si se pasa un parámetro al comando, se establece la nueva máscara.

**Modo simbólico:** permite establecer los permisos usando las letras `u` (_user_), `g` (_group_), `o` (_other_) y `a` (_all_). Se puede hacer en modo relativo usando los símbolos `+` y `-`, o en modo absoluto con `=`, y combinaciones de ambos.

```bash
# Modo relativo
umask g-w
umask a+x
# Modo relatuvo (u,o) y modo absoluto (g)
umask u-w,g=r,o+r
```

**Modo octal:** permite establecer los permisos numéricamente, siempre en modo absoluto.

El modo octal se usa en base a los permisos máximos, que para directorios es `777` y para archivos `666` (sin ejecución). Los bits de la máscara que estén a 1 desactivarán ese permiso a los permisos máximos. Ej: `umask = 023`

```bash
Umask      023: 000010011
Directorio 777: 111111111 -> 111101100 = rwxr-xr--
Archivo    666: 110110110 -> 110100100 = rw-r--r--
```

Muchos sistemas tienen la máscara `022`, que se establece con:

```bash
umask 022
```

#### Cambio de propietario y de grupo <a href="#cambio-de-propietario-y-de-grupo" id="cambio-de-propietario-y-de-grupo"></a>

Estos dos atributos se pueden modificar con los comandos:

* `chown archivo nuevo_propietario`: modifica el propietario (_UID_ asociado).
* `chgrp archivo nuevo_grupo`: modifica el grupo (_GID_ asociado).

Con ambos se puede usar la opción `-R` en directorios, para que realice la operación de manera **recursiva**, es decir, que lo aplique a todo lo que contiene directamente o en subdirectorios, sub-subdirectorios etc.

***

### Sudoers <a href="#sudoers" id="sudoers"></a>

Si el usuario intenta ejecutar algo con `sudo`, se comprueba si tiene permisos para ejecutar el comando, y si no los tiene, no lo ejecuta y el intento queda registrado en el sistema.

Se puede configurar los privilegios de los usuarios para ejecutar ciertos comandos con el fichero `/etc/sudoers`. Las modificaciones sobre este archivo no se deben realizar como si fuese un fichero normal, sino que hay que modificarlo con el comando `visudo`.

Este archivo está dividido en varias secciones:

**Definición de alias:** Existen varios tipos de alias para realizar agrupaciones. Algunos de ellos son:

*   `Cmnd_Alias`: define alias de comandos. Por ejemplo:

    ```bash
    Cmnd_Alias CMND_RED = /sbin/ifup, /sbin/ifdown
    ```
*   `User_Alias`: agrupaciones de usuarios.

    ```bash
    User_Alias ADMINS = user1, user2
    ```
*   `Host_Alias`: alias de hosts, que pueden indicarse por su nombre, IP o IP son máscara de subred.

    ```bash
    Host_Alias MIEMPRESA = 172.26.0.0/16
    ```

Si se quiere permitir acceso completo a un usuario, se puede indicar con el alias especial `ALL`. Por ejemplo, el usuario `root` se suele configurar como:

```
root ALL=(ALL) ALL
```

No es necesario reiniciar el sistema una vez modificado este fichero con `visudo`.
