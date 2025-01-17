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

# Curl

Curl es utilizado para transferir datos desde o hacia un servidor diseñado para funcionar sin interacción del usuario.

### Guarde la salida en un archivo <a href="#save-the-output-to-a-file" id="save-the-output-to-a-file"></a>

Para guardar el resultado del `curl`comando, utilice la opción `-o`o `-O`.

Las minúsculas `-o`guardan el archivo con un nombre de archivo predefinido.

```
curl -o vue-v2.6.10.js https://cdn.jsdelivr.net/npm/vue/dist/vue.js
```

Mayúsculas `-O`guarda el archivo con su nombre de archivo original:

```
curl -O https://cdn.jsdelivr.net/npm/vue/dist/vue.js
```

### Descargar varios archivos <a href="#download-multiple-files" id="download-multiple-files"></a>

Para descargar varios archivos a la vez, utilice varias `-O`opciones, seguidas de la URL del archivo que desea descargar.

En el siguiente ejemplo, estamos descargando los archivos iso de Arch Linux y Debian:

```
curl -O http://mirrors.edge.kernel.org/archlinux/iso/2018.06.01/archlinux-2018.06.01-x86_64.iso  \ -O https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-9.4.0-amd64-netinst.iso
```

### Reanudar una descarga <a href="#resume-a-download" id="resume-a-download"></a>

Puede reanudar una descarga utilizando la `-C -`opción. Esto es útil si tu conexión se cae durante la descarga de un archivo grande y, en lugar de comenzar la descarga desde cero, puedes continuar con la anterior.

Por ejemplo, si está descargando el archivo iso de Ubuntu 18.04 usando el siguiente comando:

```
curl -O http://releases.ubuntu.com/18.04/ubuntu-18.04-live-server-amd64.iso
```

y de repente tu conexión se cae, puedes reanudar la descarga con:

```
curl -C - -O http://releases.ubuntu.com/18.04/ubuntu-18.04-live-server-amd64.iso
```

### Obtener los encabezados HTTP de una URL <a href="#get-the-http-headers-of-a-url" id="get-the-http-headers-of-a-url"></a>

Los encabezados HTTP son pares clave-valor separados por dos puntos que contienen información como el agente de usuario, el tipo de contenido y la codificación. Los encabezados se pasan entre el cliente y el servidor con la solicitud o la respuesta.

Utilice la `-I`opción para recuperar solo los encabezados HTTP del recurso especificado:

```
curl -I --http2 https://www.ubuntu.com/
```

### Pruebe si un sitio web admite HTTP/2 <a href="#test-if-a-website-supports-http2" id="test-if-a-website-supports-http2"></a>

Para verificar si una URL en particular admite el nuevo [protocolo HTTP/2](https://en.wikipedia.org/wiki/HTTP/2) , busque los encabezados HTTP junto `-I`con la `--http2`opción:

```
curl -I --http2 -s https://linuxize.com/ | grep HTTP
```

La `-s`opción indica `curl`que se ejecute en silencio y que oculte el medidor de progreso y los mensajes de error.

Si el servidor remoto admite HTTP/2, `curl`imprime `HTTP/2.0 200`:

```output
HTTP/2 200
```

De lo contrario, la respuesta es `HTTP/1.1 200`:

```output
HTTP/1.1 200 OK
```

### Seguir redirecciones <a href="#follow-redirects" id="follow-redirects"></a>

De forma predeterminada, `curl`no sigue los encabezados de ubicación HTTP.

Si intentas recuperar la versión sin www de `google.com`, notarás que en lugar de obtener la fuente de la página serás redirigido a la versión con www:

```
curl google.com
```

La `-L`opción indica `curl`seguir cualquier redireccionamiento hasta llegar al destino final:

```
curl -L google.com
```

### Cambiar el agente de usuario <a href="#change-the-user-agent" id="change-the-user-agent"></a>

A veces, al descargar un archivo, el servidor remoto puede configurarse para bloquear el agente de usuario de Curl o para devolver contenidos diferentes según el dispositivo y el navegador del visitante.

En situaciones como ésta, para emular un navegador diferente, utilice la `-A`opción.

Por ejemplo, para emular Firefox 60 usarías:

```
curl -A "Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" https://getfedora.org/
```

### Especificar una tasa de transferencia máxima <a href="#specify-a-maximum-transfer-rate" id="specify-a-maximum-transfer-rate"></a>

La `--limit-rate`opción le permite limitar la velocidad de transferencia de datos. El valor se puede expresar en bytes, kilobytes con el `k`sufijo, megabytes con el `m`sufijo y gigabytes con el `g`sufijo.

En el siguiente ejemplo `curl`, descargaremos el binario de Go y limitaremos la velocidad de descarga a 1 MB:

```
curl --limit-rate 1m -O https://dl.google.com/go/go1.10.3.linux-amd64.tar.gz
```

Esta opción es útil para evitar `curl`consumir todo el ancho de banda disponible.

### Transferir archivos a través de FTP <a href="#transfer-files-via-ftp" id="transfer-files-via-ftp"></a>

Para acceder a un servidor FTP protegido con `curl`, use la `-u`opción y especifique el nombre de usuario y la contraseña como se muestra a continuación:

```
curl -u FTP_USERNAME:FTP_PASSWORD ftp://ftp.example.com/
```

Una vez que haya iniciado sesión, el comando enumera todos los archivos y directorios en el directorio de inicio del usuario.

Puede descargar un único archivo desde el servidor FTP utilizando la siguiente sintaxis:

```
curl -u FTP_USERNAME:FTP_PASSWORD ftp://ftp.example.com/file.tar.gz
```

Para cargar un archivo al servidor FTP, use `-T`seguido del nombre del archivo que desea cargar:

```
curl -T newfile.tar.gz -u FTP_USERNAME:FTP_PASSWORD ftp://ftp.example.com/
```

### Enviar cookies <a href="#send-cookies" id="send-cookies"></a>

A veces es posible que necesite realizar una solicitud HTTP con cookies específicas para acceder a un recurso remoto o para depurar un problema.

De forma predeterminada, al solicitar un recurso con `curl`, no se envían ni almacenan cookies.

Para enviar cookies al servidor, utilice el `-b`interruptor seguido de un nombre de archivo que contenga las cookies o una cadena.

```
curl -L -b "oraclelicense=a" -O http://download.oracle.com/otn-pub/java/jdk/10.0.2+13/19aef61b38124481863b1413dce1855f/jdk-10.0.2_linux-x64_bin.rpm
```

### Usando servidores proxy <a href="#using-proxies" id="using-proxies"></a>

`curl`admite diferentes tipos de servidores proxy, incluidos HTTP, HTTPS y SOCKS. Para transferir datos a través de un servidor proxy, utilice la opción `-x`( `--proxy`), seguida de la URL del proxy.

El siguiente comando descarga el recurso especificado utilizando un proxy en el `192.168.44.1`puerto `8888`:

```
curl -x 192.168.44.1:8888 http://linux.com/
```

Si el servidor proxy requiere autenticación, utilice la opción `-U`( `--proxy-user`) seguida del nombre de usuario y la contraseña separados por dos puntos ( `user:password`):

```
curl -U username:password -x 192.168.44.1:8888 http://linux.com/
```

### HTTP GET <a href="#http-get" id="http-get"></a>

```
curl https://jsonplaceholder.typicode.com/posts
```

Filtrar los resultados que utilizan parametros query:

```
curl https://jsonplaceholder.typicode.com/posts?userId=1
```

### HTTP POST <a href="#http-post" id="http-post"></a>

```
curl -X POST -d "userId=5&title=Hello World&body=Post body." https://jsonplaceholder.typicode.com/post
```

El tipo de cuerpo de la solicitud se especifica utilizando el encabezado Content-Type. Por defecto, cuando este encabezado no se proporciona, curl utiliza Content-Type: application/x-www-form-urlencoded. Para enviar un conjunto de datos con formato JSON, establezca el tipo de cuerpo en application/json.

```
curl -X POST -H "Content-Type: application/json" \    -d '{"userId": 5, "title": "Hello World", "body": "Post body."}' \    https://jsonplaceholder.typicode.com/posts
```

### HTTP PUT <a href="#http-put" id="http-put"></a>

```
curl -X PUT -d "userId=5&title=Hello World&body=Post body." https://jsonplaceholder.typicode.com/posts/5
```

### HTTP PATCH <a href="#http-patch" id="http-patch"></a>

```
curl -X PUT -d "title=Hello Universe" https://jsonplaceholder.typicode.com/posts/5
```

### HTTP DELETE <a href="#http-delete" id="http-delete"></a>

```
curl -X DELETE https://jsonplaceholder.typicode.com/posts/5
```

### Authentication <a href="#authentication" id="authentication"></a>

Si el punto final de la API requiere autenticación, deberás obtener una clave de acceso. De lo contrario, el servidor de la API responderá con el mensaje de respuesta "Acceso prohibido" o "No autorizado". El proceso para obtener una clave de acceso depende de la API que estés utilizando. Una vez que tengas tu token de acceso, puedes enviarlo en el encabezado:

```
curl -X GET -H "Authorization: Bearer {ACCESS_TOKEN}" "https://api.server.io/posts"
```

#### Cronometrar una conexión con Curl <a href="#timing-a-connection-with-curl" id="timing-a-connection-with-curl"></a>

Otra razón por la que comencé a aprender más sobre curl fue que quería ver cuánto tiempo exactamente tardaba mi sitio web en responder.

```
curl -w "%{time_total}\n" -o /dev/null -s www.example.com
```

<mark style="color:red;">**Recursos**</mark>

{% embed url="https://linuxize.com/post/curl-command-examples/#install-curl-on-centos-and-fedora" %}

{% embed url="https://linuxize.com/post/curl-rest-api/#http-get" %}

{% embed url="https://www.freecodecamp.org/news/how-to-start-using-curl-and-why-a-hands-on-introduction-ea1c913caaaa/" %}

{% embed url="https://www.digitalocean.com/community/tutorials/workflow-downloading-files-curl" %}

{% embed url="https://www.stationx.net/curl-cheat-sheet/" %}

{% embed url="https://linuxopsys.com/topics/curl-command-cheat-sheet" %}
