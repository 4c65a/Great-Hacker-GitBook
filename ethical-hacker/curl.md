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

Las minúsculas `-o`guardan el archivo con un nombre de archivo predefinido, que en el siguiente ejemplo es `vue-v2.6.10.js`:

```
curl -o vue-v2.6.10.js https://cdn.jsdelivr.net/npm/vue/dist/vue.jsCopiar
```

Mayúsculas `-O`guarda el archivo con su nombre de archivo original:

```
curl -O https://cdn.jsdelivr.net/npm/vue/dist/vue.jsCopiar
```

### Descargar varios archivos <a href="#download-multiple-files" id="download-multiple-files"></a>

Para descargar varios archivos a la vez, utilice varias `-O`opciones, seguidas de la URL del archivo que desea descargar.

En el siguiente ejemplo, estamos descargando los archivos iso de Arch Linux y Debian:

```
curl -O http://mirrors.edge.kernel.org/archlinux/iso/2018.06.01/archlinux-2018.06.01-x86_64.iso  \     -O https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-9.4.0-amd64-netinst.isoCopiarCopiar
```

### Reanudar una descarga <a href="#resume-a-download" id="resume-a-download"></a>

Puede reanudar una descarga utilizando la `-C -`opción. Esto es útil si tu conexión se cae durante la descarga de un archivo grande y, en lugar de comenzar la descarga desde cero, puedes continuar con la anterior.

Por ejemplo, si está descargando el archivo iso de Ubuntu 18.04 usando el siguiente comando:

```
curl -O http://releases.ubuntu.com/18.04/ubuntu-18.04-live-server-amd64.isoCopiar
```

y de repente tu conexión se cae, puedes reanudar la descarga con:

```
curl -C - -O http://releases.ubuntu.com/18.04/ubuntu-18.04-live-server-amd64.isoCopiar
```

### Obtener los encabezados HTTP de una URL <a href="#get-the-http-headers-of-a-url" id="get-the-http-headers-of-a-url"></a>

Los encabezados HTTP son pares clave-valor separados por dos puntos que contienen información como el agente de usuario, el tipo de contenido y la codificación. Los encabezados se pasan entre el cliente y el servidor con la solicitud o la respuesta.

Utilice la `-I`opción para recuperar solo los encabezados HTTP del recurso especificado:

```
curl -I --http2 https://www.ubuntu.com/Copiar
```

<figure><img src="https://linuxize.com/post/curl-command-examples/curl-get-http-headers_hu4f8e3f8879f6184d743f6d022f032775_44885_768x0_resize_q75_lanczos.jpg" alt="curl obtener encabezados http"><figcaption></figcaption></figure>

### Pruebe si un sitio web admite HTTP/2 <a href="#test-if-a-website-supports-http2" id="test-if-a-website-supports-http2"></a>

Para verificar si una URL en particular admite el nuevo [protocolo HTTP/2](https://en.wikipedia.org/wiki/HTTP/2) , busque los encabezados HTTP junto `-I`con la `--http2`opción:

```
curl -I --http2 -s https://linuxize.com/ | grep HTTPCopiar
```

La `-s`opción indica `curl`que se ejecute en silencio y que oculte el medidor de progreso y los mensajes de error.

Si el servidor remoto admite HTTP/2, `curl`imprime `HTTP/2.0 200`:

```output
HTTP/2 200
Copiar
```

De lo contrario, la respuesta es `HTTP/1.1 200`:

```output
HTTP/1.1 200 OK
Copiar
```

Si tiene una versión curl `7.47.0`o más reciente, no necesita usar la `--http2`opción porque HTTP/2 está habilitado de forma predeterminada para todas las conexiones HTTPS.

### Seguir redirecciones <a href="#follow-redirects" id="follow-redirects"></a>

De forma predeterminada, `curl`no sigue los encabezados de ubicación HTTP.

Si intentas recuperar la versión sin www de `google.com`, notarás que en lugar de obtener la fuente de la página serás redirigido a la versión con www:

```
curl google.comCopiar
```

<figure><img src="https://linuxize.com/post/curl-command-examples/curl-follow-redirects_hu91e18c75b5146489a4e207dd1e58d4a1_29252_768x0_resize_q75_lanczos.jpg" alt="curl seguir redirecciones"><figcaption></figcaption></figure>

La `-L`opción indica `curl`seguir cualquier redireccionamiento hasta llegar al destino final:

```
curl -L google.comCopiar
```

### Cambiar el agente de usuario <a href="#change-the-user-agent" id="change-the-user-agent"></a>

A veces, al descargar un archivo, el servidor remoto puede configurarse para bloquear el agente de usuario de Curl o para devolver contenidos diferentes según el dispositivo y el navegador del visitante.

En situaciones como ésta, para emular un navegador diferente, utilice la `-A`opción.

Por ejemplo, para emular Firefox 60 usarías:

```
curl -A "Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0" https://getfedora.org/Copiar
```

### Especificar una tasa de transferencia máxima <a href="#specify-a-maximum-transfer-rate" id="specify-a-maximum-transfer-rate"></a>

La `--limit-rate`opción le permite limitar la velocidad de transferencia de datos. El valor se puede expresar en bytes, kilobytes con el `k`sufijo, megabytes con el `m`sufijo y gigabytes con el `g`sufijo.

En el siguiente ejemplo `curl`, descargaremos el binario de Go y limitaremos la velocidad de descarga a 1 MB:

```
curl --limit-rate 1m -O https://dl.google.com/go/go1.10.3.linux-amd64.tar.gzCopiar
```

Esta opción es útil para evitar `curl`consumir todo el ancho de banda disponible.

### Transferir archivos a través de FTP <a href="#transfer-files-via-ftp" id="transfer-files-via-ftp"></a>

Para acceder a un servidor FTP protegido con `curl`, use la `-u`opción y especifique el nombre de usuario y la contraseña como se muestra a continuación:

```
curl -u FTP_USERNAME:FTP_PASSWORD ftp://ftp.example.com/Copiar
```

Una vez que haya iniciado sesión, el comando enumera todos los archivos y directorios en el directorio de inicio del usuario.

Puede descargar un único archivo desde el servidor FTP utilizando la siguiente sintaxis:

```
curl -u FTP_USERNAME:FTP_PASSWORD ftp://ftp.example.com/file.tar.gzCopiar
```

Para cargar un archivo al servidor FTP, use `-T`seguido del nombre del archivo que desea cargar:

```
curl -T newfile.tar.gz -u FTP_USERNAME:FTP_PASSWORD ftp://ftp.example.com/Copiar
```

### Enviar cookies <a href="#send-cookies" id="send-cookies"></a>

A veces es posible que necesite realizar una solicitud HTTP con cookies específicas para acceder a un recurso remoto o para depurar un problema.

De forma predeterminada, al solicitar un recurso con `curl`, no se envían ni almacenan cookies.

Para enviar cookies al servidor, utilice el `-b`interruptor seguido de un nombre de archivo que contenga las cookies o una cadena.

[Por ejemplo, para descargar el archivo rpm](https://linuxize.com/post/how-to-install-rpm-packages-on-centos/) de Oracle Java JDK `jdk-10.0.2_linux-x64_bin.rpm`, deberá pasar una cookie denominada `oraclelicense`con valor `a`:

```
curl -L -b "oraclelicense=a" -O http://download.oracle.com/otn-pub/java/jdk/10.0.2+13/19aef61b38124481863b1413dce1855f/jdk-10.0.2_linux-x64_bin.rpmCopiar
```

### Usando servidores proxy <a href="#using-proxies" id="using-proxies"></a>

`curl`admite diferentes tipos de servidores proxy, incluidos HTTP, HTTPS y SOCKS. Para transferir datos a través de un servidor proxy, utilice la opción `-x`( `--proxy`), seguida de la URL del proxy.

El siguiente comando descarga el recurso especificado utilizando un proxy en el `192.168.44.1`puerto `8888`:

```
curl -x 192.168.44.1:8888 http://linux.com/Copiar
```

Si el servidor proxy requiere autenticación, utilice la opción `-U`( `--proxy-user`) seguida del nombre de usuario y la contraseña separados por dos puntos ( `user:password`):

```
curl -U username:password -x 192.168.44.1:8888 http://linux.com/Copiar
```

\
