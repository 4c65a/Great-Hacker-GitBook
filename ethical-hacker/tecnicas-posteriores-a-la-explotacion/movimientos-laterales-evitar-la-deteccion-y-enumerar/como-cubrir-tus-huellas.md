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

# Cómo cubrir tus huellas

Después de comprometer un sistema durante una prueba de penetración, siempre debe cubrir sus pistas para evitar la detección suprimiendo registros, eliminando cuentas de usuario que podrían haberse creado en el sistema y eliminando cualquier archivo que se haya creado. Además, una vez finalizada la prueba de penetración, debe limpiar todos los sistemas. Como mejor práctica, debe discutir estas tareas y documentarlas en el documento de reglas de participación durante la fase previa al compromiso. Las siguientes son algunas de las mejores prácticas a tener en cuenta durante el proceso de limpieza:

* Elimine todas las cuentas de usuario utilizadas durante la prueba.
* Elimine todos los archivos, binarios ejecutables, scripts y archivos temporales de los sistemas comprometidos. Es posible que se prefiera un método de eliminación seguro. Publicación especial del NIST 800-88, Revisión 1: “Pautas para la desinfección de medios”, proporciona orientación para la desinfección de medios. Esta metodología debe discutirse con su cliente y el propietario de los sistemas afectados.
* Devuelva cualquier sistema modificado y su configuración a sus valores y parámetros originales.
* Elimine todas las puertas traseras, demonios, servicios y rootkits instalados.
* Elimine todos los datos de los clientes de sus sistemas, incluidos los sistemas atacantes y cualquier otro sistema de soporte. Normalmente, debe hacer esto después de crear y entregar el informe de prueba de penetración al cliente.

**Steganography**

Los atacantes pueden utilizar la esteganografía para ofuscar, evadir y cubrir sus huellas. La esteganografía implica ocultar un mensaje o cualquier otro contenido dentro de una imagen o un archivo de video. Para realizar esta tarea, puedes utilizar herramientas como steghide . Puede instalar fácilmente esta herramienta en un sistema Linux basado en Debian.

_Uso del comando **steghide**_

```
|--[omar@websploit]-[~]
|---- $steghide --help
steghide version 0.5.1

the first argument must be one of the following:
 embed, --embed             embed data
 extract, --extract        extract data
 info, --info                display information about a cover- or
                               stego-file
   info <filename>          display information about <filename>
 encinfo, --encinfo        display a list of supported encryption
                               algorithms
 version, --version        display version information
 license, --license        display steghide’s license
 help, --help               display this usage information

embedding options:
 -ef, --embedfile          select file to be embedded
   -ef <filename>          embed the file <filename>
 -cf, --coverfile          select cover-file
   -cf <filename>          embed into the file <filename>
 -p, --passphrase          specify passphrase
   -p <passphrase>         use <passphrase> to embed data
 -sf, --stegofile          select stego file
   -sf <filename>          write result to <filename> instead of
                              cover-file
 -e, --encryption          select encryption parameters
   -e <a>[<m>]|<m>[<a>]   specify an encryption algorithm and/or mode
   -e none                   do not encrypt data before embedding
 -z, --compress            compress data before embedding (default)
   -z <l>                    using level <l> (1 best speed...9 best
                              compression)
 -Z, --dontcompress        do not compress data before embedding
 -K, --nochecksum          do not embed crc32 checksum of embedded data
 -N, --dontembedname       do not embed the name of the original file
 -f, --force                 overwrite existing files
 -q, --quiet                 suppress information messages
 -v, --verbose              display detailed information

extracting options:
 -sf, --stegofile          select stego file
   -sf <filename>          extract data from <filename>
 -p, --passphrase          specify passphrase
   -p <passphrase>         use <passphrase> to extract data
 -xf, --extractfile        select file name for extracted data
   -xf <filename>           write the extracted data to <filename>
 -f, --force                overwrite existing files
 -q, --quiet                suppress information messages
 -v, --verbose              display detailed information

options for the info command:
 -p, --passphrase          specify passphrase
   -p <passphrase>         use <passphrase> to get info about
                              embedded data

To embed emb.txt in cvr.jpg: steghide embed -cf cvr.jpg -ef emb.txt
To extract embedded data from stg.jpg: steghide extract -sf stg.jpg
|--[omar@websploit]-[~]
|---- $

```

Echemos un vistazo a un ejemplo de cómo incrustar información confidencial y ocultar un mensaje dentro de un archivo de imagen mediante el uso de esteganografía. En el ejemplo 8-11, un archivo llamado secret.txt incluye información confidencial (datos de tarjetas de crédito) que se extraerá mediante esteganografía.

_**Ejemplo 8-11**_ _: Datos confidenciales que se ocultarán mediante esteganografía_

```

|--[omar@websploit]-[~]
|---- $cat secret.txt
Credit card data:
4011 5555 5555 5555 5555 exp 08/29 ccv: 123
4021 6666 7777 8888 9999 exp 02/29 ccv: 321

|--[omar@websploit]-[~]
|---- $ 

```

El ejemplo 8-12 muestra cómo incrustar estos datos confidenciales (secret.txt) en un archivo de imagen (websploit-logo.png) usando **steghide** .

_**Ejemplo 8-12**_ _: uso **de steghide**_ _para ocultar datos confidenciales en un archivo de imagen_

```
|--[omar@websploit]-[~]
|---- $steghide embed -ef secret.txt -cf websploit-logo.jpg
Enter passphrase: this-is-a-passphrase
Re-Enter passphrase: this-is-a-passphrase
embedding "secret.txt" in "websploit-logo.jpg"... done
|--[omar@websploit]-[~]
|---- $ 
```

El ejemplo 8-13 muestra cómo se recuperan los datos confidenciales de la imagen y se guardan en un archivo ( **extraído\_datos.txt** ).

_**Ejemplo 8-13**_ _: Extracción de datos ocultos de un archivo de imagen_

```
|--[omar@websploit] ⊠[~]
|---- $steghide extract -sf websploit-logo.jpg -xf extracted_data.txt
Enter passphrase: this-is-a-passphrase
wrote extracted data to "extracted_data.txt".

```

El ejemplo 8-14 muestra el contenido del archivo de datos extraído (extracto\_datos.txt).

_**Ejemplo 8-14**_ _: El contenido del archivo de datos extraído_

```
|--[omar@websploit]-[~]
|---- $cat extracted_data.txt
Credit card data:
4011 5555 5555 5555 5555 exp 08/29 ccv: 123
4021 6666 7777 8888 9999 exp 02/29 ccv: 321
|--[omar@websploit]-[~]
|----$
```

