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

    ```
    $ id -u   # Imprime el UID
    $ id -un  # Imprime el login
    ```
* `chage` – _change age_ visualiza y modifica todas las fechas de contraseña de `/etc/shadow`.

También existen los comandos `adduser` y `deluser` que son más _user-friendly_ y ahorran algo de trabajo, por lo que se utilizan con más frecuencia en la práctica.

> Usa el manual `man` o las opciones `-h` o `--help` para ver todas las opciones que ofrecen estos comandos, ya que pueden cambiar según distribuciones.

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

```
# Modificar el grupo primario
$ usermod -g GROUP USER
$ # Reemplazar el grupo secundario
$ usermod -G GROUP USER
$ # Añadir un grupo secundario al usuario
$ usermod -a -G GROUP USER
```

#### Modificaciones de permisos <a href="#modificaciones-de-permisos" id="modificaciones-de-permisos"></a>

Los permisos de un archivo o directorio se pueden modificar con el comando:

```
$ chmod permisos archivo(s)
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

```
$ chmod u+x fichero
$ chmod go-x fichero
$ chmod +x fichero
```

**Modo absoluto.** Se puede reemplazar la información completa de los permisos utilizando un número en base 8 (octal) de tres cifras. Los permisos coinciden con los del número en binario. Lo bueno de trabajar en octal es que cada caracter se puede trabajar de manera independiente.

Ejemplo de permiso `754`:

* `7` en binario es `111` ⇒ permisos de _usuario_: `rwx`
* `5` en binario es `101` ⇒ permisos de _grupo_: `r-x`
* `4` en binario es `100` ⇒ permisos de _otros_: `r--`

```
$ chmod 754 file
$ ls -l file
-rwxr-xr-- 1 usuario grupo  2048 Jan  6 13:03 file
```

#### Máscara `umask` <a href="#mascara-umask" id="mascara-umask"></a>

La máscara del sistema operativo define los permisos que se asignan por defecto a archivos y directorios en el momento de su creación.

El comando `umask` sin parámetros imprime el valor que tiene actualmente, y se puede manejar en modo simbólico y modo octal:

```
$ umask
0022
$ umask -S
u=rwx,g=rx,o=rx
```

Si se pasa un parámetro al comando, se establece la nueva máscara.

**Modo simbólico:** permite establecer los permisos usando las letras `u` (_user_), `g` (_group_), `o` (_other_) y `a` (_all_). Se puede hacer en modo relativo usando los símbolos `+` y `-`, o en modo absoluto con `=`, y combinaciones de ambos.

```
$ # Modo relativo
$ umask g-w
$ umask a+x
$ # Modo relatuvo (u,o) y modo absoluto (g)
$ umask u-w,g=r,o+r
```

**Modo octal:** permite establecer los permisos numéricamente, siempre en modo absoluto.

El modo octal se usa en base a los permisos máximos, que para directorios es `777` y para archivos `666` (sin ejecución). Los bits de la máscara que estén a 1 desactivarán ese permiso a los permisos máximos. Ej: `umask = 023`

```
Umask      023: 000010011
Directorio 777: 111111111 -> 111101100 = rwxr-xr--
Archivo    666: 110110110 -> 110100100 = rw-r--r--
```

Muchos sistemas tienen la máscara `022`, que se establece con:

```
$ umask 022
```

#### Cambio de propietario y de grupo <a href="#cambio-de-propietario-y-de-grupo" id="cambio-de-propietario-y-de-grupo"></a>

Estos dos atributos se pueden modificar con los comandos:

* `chown archivo nuevo_propietario`: modifica el propietario (_UID_ asociado).
* `chgrp archivo nuevo_grupo`: modifica el grupo (_GID_ asociado).

Con ambos se puede usar la opción `-R` en directorios, para que realice la operación de manera **recursiva**, es decir, que lo aplique a todo lo que contiene directamente o en subdirectorios, sub-subdirectorios etc.

***

### Sudoers <a href="#sudoers" id="sudoers"></a>

En Linux se pueden ejecutar determinados comandos como si fuesen el _root_ con `sudo comando`. Si el usuario intenta ejecutar algo con `sudo`, se comprueba si tiene permisos para ejecutar el comando, y si no los tiene, no lo ejecuta y el intento queda registrado en el sistema.

Se puede configurar los privilegios de los usuarios para ejecutar ciertos comandos con el fichero `/etc/sudoers`. Las modificaciones sobre este archivo no se deben realizar como si fuese un fichero normal, sino que hay que modificarlo con el comando `visudo`.

Este archivo está dividido en varias secciones:

**Definición de alias:** Existen varios tipos de alias para realizar agrupaciones. Algunos de ellos son:

*   `Cmnd_Alias`: define alias de comandos. Por ejemplo:

    ```
    Cmnd_Alias CMND_RED = /sbin/ifup, /sbin/ifdown
    ```
*   `User_Alias`: agrupaciones de usuarios.

    ```
    User_Alias ADMINS = user1, user2
    ```
*   `Host_Alias`: alias de hosts, que pueden indicarse por su nombre, IP o IP son máscara de subred.

    ```
    Host_Alias MIEMPRESA = 172.26.0.0/16
    ```

**Reglas de acceso:** En esta sección se asignan a los comandos que pueden realizar los usuarios y desde qué hosts lo puede hacer.

Tiene el formato:

```
usuario host = (usuario_privilegiado) comandos
```

* **Usuario:** puede ser un usuario o alias de usuario. Indica a quién afecta la regla. Si comienza por `%`, entonces el nombre se refiere a un grupo del sistema.
* **Host:** indica desde qué host se permiten realizar esos comandos.
* **Usuario\_privilegiado:** indica qué permisos de usuarios privilegiados se permiten al usuario. Este campo es opcional.
* **Comandos:** indica los comandos o alias de comandos que se permiten para el usuario.

Es necesario escribir los comandos usando su ruta completa. Para consultar la ruta de un comando puedes usar `which <nombre_comando>`. Los comandos más comunes se suelen localizar en:

| `/bin`           | comandos **esenciales** del sistema (`cat`, `ls`…) accesibles desde una etapa muy temprana en el arranque del sistema. Son accesibles por todos los usuarios. |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/sbin`          | lo mismo, pero que requieren permisos de superusuario.                                                                                                        |
| `/usr/bin`       | comandos **no esenciales**, pero de uso general instalados a nivel de sistema para todos los usuarios.                                                        |
| `/usr/sbin`      | equivalente al anterior, pero que requiere permisos de superusuario.                                                                                          |
| `/usr/local/bin` | comandos que no forman parte de la distribución del SO.                                                                                                       |

Por ejemplo:

```
ADMINS MIEMPRESA = CMND_RED
```

Si se quiere permitir acceso completo a un usuario, se puede indicar con el alias especial `ALL`. Por ejemplo, el usuario `root` se suele configurar como:

```
root ALL=(ALL) ALL
```

No es necesario reiniciar el sistema una vez modificado este fichero con `visudo`. Una vez configurado, un usuario podrá ejecutar esos comandos permitidos con `sudo` usando su propia contraseña.
