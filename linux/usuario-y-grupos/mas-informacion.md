# Mas informacion

| Símbolo | Tipo de archivo    | Descripción                                                                    |
| ------- | ------------------ | ------------------------------------------------------------------------------ |
| `d`     | directorio         | Un archivo usado para contener otros archivos.                                 |
| `-`     | archivo ordinario  | Incluye archivos leíbles, imágenes, archivos binarios, y archivos comprimidos. |
| `l`     | enlaces simbólicos | Apunta a otro archivo.                                                         |
| `s`     | socket             | Permite la comunicación entre procesos.                                        |
| `p`     | tubería (pipe)     | Permite la comunicación entre procesos.                                        |
| `b`     | archivo bloque     | Usado para comunicaciones con el equipo (hardware).                            |
| `c`     | archivo carácter   | Usado para comunicaciones con el equipo (hardware).                            |

### Permisos

Los permisos determinan la forma en que los diferentes usuarios pueden interactuar con un archivo o directorio. Al enumerar un archivo con el comando `ls -l`, el resultado incluye información sobre sus permisos. Para nuestro ejemplo usaremos un script llamado `hello.sh` ubicado en el directorio `Documents`:                           &#x20;

```
-rw-r--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh
```

#### Tipo de archivo

```
-rw-r--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh
```

El primer carácter de esta salida indica el tipo de archivo. Recuerde que si el primer carácter es un `-`, este es un archivo ordinario. Si el carácter fuera una `d`, se trataría de un directorio.

```
-rw-r--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh
```

Después del carácter de tipo de archivo, se muestran los permisos. Los permisos se dividen en tres grupos de tres caracteres:

1.  #### Propietario

    ```
    -rw-r--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh
    ```

    El primer grupo se refiere al usuario que posee el archivo. Si su cuenta actual es la propietaria del archivo, se usará el primer grupo de permisos y los demás permisos no tendrán efecto.

    El usuario propietario del archivo y a quién se refieren estos permisos se puede determinar mediante el campo que muestra el usuario propietario:
2.  #### Grupo

    ```
    -rw-r--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh
    ```

    El segundo conjunto se refiere al grupo que posee el archivo. Si su cuenta actual no es la del propietario del archivo pero es miembro del grupo que posee el archivo, se aplicarán los permisos del grupo y los demás permisos no tendrán efecto.
3.  #### Otros

    ```
    -rw-r--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh
    ```

    El último grupo es para todos los demás, cualquiera a quien los dos primeros conjuntos de permisos no sean aplicables. Si no es el usuario que posee el archivo o un miembro del grupo que posee el archivo, se le aplicará el tercer conjunto de permisos.

#### Tipos de permisos

Un archivo o directorio puede presentar tres permisos diferentes: leer, escribir y ejecutar. La forma en que se aplican estos permisos difiere entre archivos y directorios, como se muestra en la tabla siguiente:

| Permiso                  | Efectos sobre los Archivos                                                                                         | Efectos sobre los Directorios                                                                                                                                                                           |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| leer (read) (`r`)        | Permite que el contenido del archivo sea leído o copiado.                                                          | Sin el permiso para ejecutar, permite obtener un listado poco detallado de los archivos que contiene el directorio. Con el permiso para ejecutar, `ls -l` proporciona un listado detallado de archivos. |
| escribir (write) (`w`)   | Permite modificar o reescribir el contenido del archivo. Permite añadir o eliminar archivos en un directorio.      | Para que este permiso funcione, el directorio debe tener permiso para ejecutar.                                                                                                                         |
| ejecutar (execute) (`x`) | Permite que un archivo funcione como un proceso, aunque archivos script también requerirán el permiso leer (read). | Permite que el usuario se traslade del directorio si en el directorio padre también posee permiso escribir (write).                                                                                     |

**A tener en cuenta**

Comprender qué permisos se aplican en cada momento es una aptitud importante cuando trabajamos con Linux.&#x20;

```
-r--rw-rwx. 1 sysadmin staff 999 Apr  10  2013 /home/sysadmin/test
```

En este escenario, el usuario `sysadmin` termina teniendo menos acceso a este archivo que los miembros del grupo `staff` o todos los demás. El usuario `sysadmin` sólo tiene los permisos de `r--`. No importa si `sysadmin` es miembro del grupo `staff`; una vez establecida la propiedad del usuario, solo se aplican los permisos del usuario propietario.

### Cambiar los permisos de los archivos

El comando `chmod` se utiliza para cambiar los permisos de un archivo o directorio. Sólo el usuario raíz o el usuario propietario del archivo puede cambiar los permisos de un archivo.

**Considere esto**

Hay dos métodos para cambiar permisos usando el comando `chmod`: el método simbólico y el método octal. El método simbólico es útil para cambiar un conjunto de permisos a la misma vez. El método octal o numérico requiere conocer el valor octal de cada uno de los permisos y requiere que los tres conjuntos de permisos (usuario, grupo, otros) se especifiquen cada vez. Para simplificar las cosas, solamente trataremos el método simbólico.

### Comandos

Para usar el método simbólico de `chmod` primero debe indicar qué conjunto de permisos se está cambiando:

```
chmod [<CONJUNTO DE PERMISOS><ACCIÓN><PERMISOS>]... ARCHIVO
```

| Símbolo | Significado                                                                                 |
| ------- | ------------------------------------------------------------------------------------------- |
| `u`     | Usuario: El usuario propietario del archivo.                                                |
| `g`     | Grupo: El grupo propietario del archivo.                                                    |
| `o`     | Otros: Cualquier otro que no sea el usuario propietario o un miembro del grupo propietario. |
| `a`     | Todos: Se refiere al usuario, grupo, y todos los demás.                                     |

A continuación, especifique un símbolo para la acción:

```
chmod [<CONJUNTO DE PERMISOS><ACCIÓN><PERMISOS>]... ARCHIVO
```

| Símbolo | Significado                          |
| ------- | ------------------------------------ |
| `+`     | Añadir permiso, si es necesario      |
| `=`     | Especificar el permiso exacto        |
| `-`     | Eliminar el permiso, si es necesario |

Después del símbolo de acción, especifique uno o más permisos.

```
chmod [<CONJUNTO DE PERMISOS><ACCIÓN><PERMISOS>]... ARCHIVO
```

| Símbolo | Significado        |
| ------- | ------------------ |
| `r`     | leer (read)        |
| `w`     | escribir (write)   |
| `x`     | ejecutar (execute) |

Finalmente, añada un espacio y los nombres de ruta para los archivos a los que quiere asignar los permisos.

```
chmod [<CONJUNTO DE PERMISOS><ACCIÓN><PERMISOS>]... ARCHIVO
```

El archivo `hello.sh`                       &#x20;

```
-rw-r--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh
```

Sin embargo, actualmente, el permiso de ejecución no ha sido establecido para ninguno de los grupos de permisos:

```
-rw-r--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh
```

Dado que el sistema está actualmente conectado como usuario `sysadmin`, y `sysadmin` es el propietario de este archivo, otorgar el permiso de ejecución al usuario propietario debería permitirle ejecutar este script. Usando el comando `chmod` con el carácter `u` para representar el conjunto de permisos del usuario propietario, y agregando el carácter `+` para indicar que se añade ­un permiso y el carácter `x` para representar el permiso de ejecución, el comando deberá ejecutarse con la siguiente sintaxis:

<pre><code><strong>chmod u+x hello.sh
</strong></code></pre>

No obtener un resultado/mensaje indica que el comando se ha realizado correctamente. Confírmelo examinando los permisos con el comando `ls -l`:

<pre><code><strong>sysadmin@localhost:~/Documents$ ls -l hello.sh                                  
</strong><strong>-rwxr--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh
</strong></code></pre>

El usuario propietario ahora posee permiso para ejecutar:

```
-rwxr--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh
```
