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

**Uso del comando steghide**

```
|--[omar@websploit]-[~]
|---- $steghide --help

```

Echemos un vistazo a un ejemplo de cómo incrustar información confidencial y ocultar un mensaje dentro de un archivo de imagen mediante el uso de esteganografía. n archivo llamado secret.txt incluye información confidencial que se extraerá mediante esteganografía.

**Datos confidenciales que se ocultan mediante esteganografía.**

```

|--[omar@websploit]-[~]
|---- $cat secret.txt
Credit card data:
4011 5555 5555 5555 5555 exp 08/29 ccv: 123
4021 6666 7777 8888 9999 exp 02/29 ccv: 321

```

_**Uso de steghide**_ _**para ocultar datos confidenciales en un archivo de imagen.**_

```
|--[omar@websploit]-[~]
|---- $steghide embed -ef secret.txt -cf websploit-logo.jpg
Enter passphrase: this-is-a-passphrase
Re-Enter passphrase: this-is-a-passphrase
embedding "secret.txt" in "websploit-logo.jpg"... done
|--[omar@websploit]-[~]
|---- $ 
```

**Extracción de datos ocultos de un archivo de imagen.**

```
|--[omar@websploit] ⊠[~]
|---- $steghide extract -sf websploit-logo.jpg -xf extracted_data.txt
Enter passphrase: this-is-a-passphrase
wrote extracted data to "extracted_data.txt".

```

**Muestra el contenido del archivo de datos extraído (extracto\_datos.txt).**

```
|--[omar@websploit]-[~]
|---- $cat extracted_data.txt
Credit card data:
4011 5555 5555 5555 5555 exp 08/29 ccv: 123
4021 6666 7777 8888 9999 exp 02/29 ccv: 321
|--[omar@websploit]-[~]
|----$
```

