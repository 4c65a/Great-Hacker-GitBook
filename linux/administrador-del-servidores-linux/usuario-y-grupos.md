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
