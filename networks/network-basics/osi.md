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

# OSI

El modelo Open Systems Interconnection (OSI) , el OSI proporciona un estándar para que distintos sistemas de equipos puedan comunicarse entre sí.

**7.Capa de aplicación**

Esta es la única capa que interactúa directamente con los datos del usuario. Las aplicaciones de software, como navegadores web y clientes de correo electrónico, dependen de la capa de aplicación para iniciar comunicaciones, la capa de aplicación es responsable de los protocolos y la manipulación de datos de los que depende el software para presentar datos significativos al usuario.

Los protocolos de la capa de aplicación:

```
HTTP
FTP
SMTP
DNS
Telnet
SSH
POP3
IMAP
```

**6. Capa de presentación**

La capa de presentación es responsable de la traducción, el cifrado y la compresión de los datos.

Dos dispositivos de comunicación que se conectan entre sí podrían estar usando distintos métodos de codificación, por lo que la capa 6 es la responsable de traducir los datos entrantes en una sintaxis que la capa de aplicación del dispositivo receptor pueda comprender.

Si los dispositivos se comunican a través de una conexión cifrada, la capa 6 es responsable de añadir el cifrado en el extremo del emisor, así como de decodificar el cifrado en el extremo del receptor, para poder presentar a la capa de aplicación datos descifrados y legibles.

Después, la capa de presentación es también la encargada de comprimir los datos que recibe de la capa de aplicación antes de ser enviados a la capa 5. Esto ayuda a mejorar la velocidad y la eficiencia de la comunicación mediante la minimización de la cantidad de datos que serán transferidos.

**5. Capa de sesión**

La capa de sesión es la responsable de la apertura y cierre de comunicaciones entre dos dispositivos. Ese tiempo que transcurre entre la apertura de la comunicación y el cierre de esta se conoce como sesión. La capa de sesión garantiza que la sesión permanezca abierta el tiempo suficiente como para transferir todos los datos que se están intercambiando; tras esto, cerrará sin demora la sesión para evitar desperdicio de recursos.

La capa de sesión también sincroniza la transferencia de datos utilizando puntos de control.&#x20;

**4. Capa de transporte**

La capa 4 es la responsable de las comunicaciones de extremo a extremo entre dos dispositivos. Esto implica, antes de proceder a ejecutar el envío a la capa 3, tomar datos de la capa de sesión y fragmentarlos seguidamente en trozos más pequeños llamados segmentos. La capa de transporte del dispositivo receptor es la responsable luego de rearmar tales segmentos y construir con ellos datos que la capa de sesión pueda consumir.

La capa de transporte también es responsable del control de flujo y el control de errores. El control de flujo determina una velocidad óptima de transmisión para garantizar que un emisor con una conexión rápida no abrume a un receptor con una conexión lenta. La capa de transporte realiza un control de errores en el extremo receptor al garantizar que los datos recibidos estén completos y solicitar una retransmisión si no lo están.

Los protocolos de la capa de transporte incluyen el Protocolo de control de transmisión (TCP) y el User Datagram Protocol (UDP).

**3. Capa de red**

La capa de red es responsable de facilitar la transferencia de datos entre dos redes diferentes. Si los dispositivos que se comunican se encuentran en la misma red, entonces la capa de red no es necesaria. Esta capa divide los segmentos de la capa de transporte en unidades más pequeñas, llamadas paquetes, en el dispositivo del emisor, y vuelve a juntar estos paquetes en el dispositivo del receptor. La capa de red también busca la mejor ruta física para que los datos lleguen a su destino; esto se conoce como enrutamiento.

Esta capa de red proporciona servicios para permitir que los dispositivos finales intercambien datos a través de redes. IP versión 4 (IPv4) e IP versión 6 (IPv6) son los principales protocolos de comunicación de la capa de red. Otros protocolos de capa de red incluyen protocolos de enrutamiento como Open Shortest Path First (OSPF) y protocolos de mensajería como Internet Control Message Protocol (ICMP).

Los protocolos de la capa de red realizan cuatro operaciones:

* **Direccionamiento de dispositivos finales** - Los dispositivos finales deben configurarse con una dirección IP única para la identificación en la red.
* **Encapsulación** - La capa de red encapsula la unidad de datos de protocolo (PDU) de la capa de transporte en un paquete. El proceso de encapsulamiento agrega información del encabezado IP, como la dirección IP de los hosts de origen (emisores) y de destino (receptores). El proceso de encapsulación lo realiza la fuente del paquete IP.
* **Enrutamiento** - La capa de red proporciona servicios para dirigir los paquetes a un host de destino en otra red. La función del router debe dirigir los paquetes al host de destino en un proceso que se denomina "enrutamiento". Un paquete puede cruzar muchos routers antes de llegar al host de destino. Se denomina "salto" a cada router que cruza un paquete antes de alcanzar el host de destino.
* **Desencapsulación** - Cuando el paquete llega a la capa de red del host de destino, el host verifica el encabezado IP del paquete. Si la dirección IP de destino dentro del encabezado coincide con su propia dirección IP, se elimina el encabezado IP del paquete. Una vez que la capa de red desencapsula el paquete, la PDU de capa 4 que se obtiene se transfiere al servicio apropiado en la capa de transporte.&#x20;

**2. Capa de enlace de datos**

La capa de enlace de datos es muy similar a la capa de red, excepto que la capa de enlace de datos facilita la transferencia de datos entre dos dispositivos dentro la _misma_ red. La capa de enlace de datos toma los paquetes de la capa de red y los divide en partes más pequeñas que se denominan tramas. Al igual que la capa de red, esta capa también es responsable del control de flujo y el control de errores en las comunicaciones dentro de la red (la capa de transporte solo realiza tareas de control de flujo y de control de errores para las comunicaciones dentro de la red).

**1. Capa física**

Esta capa incluye el equipo físico implicado en la transferencia de datos, tal como los cables y los conmutadores de red. Esta también es la capa donde los datos se convierten en una secuencia de bits, es decir, una cadena de unos y ceros. La capa física de ambos dispositivos también debe estar de acuerdo en cuanto a una convención de señal para que los 1 puedan distinguirse de los 0 en ambos dispositivos.
