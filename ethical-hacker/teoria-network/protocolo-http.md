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

# Protocolo HTTP

## Hypertext Transfer Protocol:

El protocolo HTTP permite realizar una petición de datos y recursos, como HTML. Es la base de cualquier intercambio de datos en la Web, y un protocolo de estructura cliente-servidor, esto quiere decir que una petición de datos es iniciada por el elemento que recibirá los datos , normalmente un navegador Web. Así, una página web completa resulta de la unión de distintos sub-documentos recibidos.

### Los servidores proxy&#x20;

Los servidores proxy HTTP actúan como servidores y clientes. Los servidores proxy realizan solicitudes a servidores web en nombre de otros clientes. Permiten transferencias HTTP a través de firewalls y también pueden brindar soporte para el almacenamiento en caché de mensajes HTTP. Los servidores proxy pueden desempeñar otras funciones en entornos complejos, incluida la traducción de direcciones de red (NAT) y el filtrado de solicitudes HTTP.

<img src="../../.gitbook/assets/file.excalidraw (1).svg" alt="" class="gitbook-drawing">

Cuando los servidores HTTP y los navegadores se comunican entre sí, realizan interacciones basadas en encabezados y contenido del cuerpo.

* **El método:** El método es HTTP **GET** , aunque podría ser cualquiera de los siguientes:\
  \- **GET:** Recupera información del servidor\
  \- **HEAD:** Solo devuelve encabezados HTTP y ningún cuerpo del documento\
  \- **POST :** Envía datos al servidor (normalmente usando formularios HTML, solicitudes API, etc.)\
  \- **TRACE:** Realiza una prueba de bucle invertido de mensajes a lo largo de la ruta al recurso de destino\
  \- **PUT:** Carga una representación del URI especificado\
  \- **DELETE:** Elimina el especificado recurso\
  \- **OPCIONES:** Devuelve los métodos HTTP que admite el servidor\
  \- **CONECTAR:** Convierte la conexión de solicitud en un túnel TCP/IP transparente.
* **El URI y path-to-resource field:** Esto representa la parte de la ruta de la URL solicitada.
* **El campo de version-number field::** Especifica la versión de HTTP utilizada por el cliente.
* **El user agent:** Se utilizó Chrome para acceder al sitio web.&#x20;
* **También aparecen varios otros campos:  accept, accept-language, accept encoding.**



