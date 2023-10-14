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

# ICMPv4 e ICMPv6

El protocolo ICMP está disponible tanto para IPv4 como para IPv6. El protocolo de mensajes para IPv4 es ICMPv4. ICMPv6 proporciona estos mismos servicios para IPv6, pero incluye funcionalidad adicional. En este curso, el término ICMP se utilizará para referirse tanto a ICMPv4 como a ICMPv6.

Los tipos de mensajes ICMP y las razones por las que se envían son extensos. Los mensajes ICMP comunes a ICMPv4 e ICMPv6 y discutidos en este módulo incluyen:

* Accesibilidad al host
* Destino o servicio inaccesible
* Tiempo superado

Se puede utilizar un mensaje de eco ICMP para probar la accesibilidad de un host en una red IP. El host local envía una solicitud de eco ICMP a un host. Si el host se encuentra disponible, el host de destino responde con una respuesta de eco. En la ilustración, haga clic en el botón Reproducir para ver una animación de la solicitud de eco/respuesta de eco ICMP. Este uso de los mensajes ICMP Echo es la base de la utilidad ping.

Los routers utilizan los mensajes de tiempo superado de ICMPv4 para indicar que un paquete no puede reenviarse debido a que el campo de tiempo de duración (TTL) del paquete se disminuyó a 0. Si un router recibe un paquete y disminuye el campo TTL en el paquete IPV4 a cero, descarta el paquete y envía un mensaje de tiempo superado al host de origen.

ICMPv6 también envía un mensaje de tiempo superado si el router no puede reenviar un paquete IPv6 debido a que el paquete caducó. En lugar del campo TTL de IPv4, ICMPv6 usa el campo Límite de salto de IPv6 para determinar si el paquete ha expirado.



Ping es una utilidad de prueba de IPv4 e IPv6 que utiliza la solicitud de eco ICMP y los mensajes de respuesta de eco para probar la conectividad entre los hosts.

Para probar la conectividad con otro host de una red, se envía una solicitud de eco a la dirección de host mediante el comando **ping**. Si el host en la dirección especificada recibe la solicitud de eco, responde con una respuesta de eco. A medida que se recibe cada respuesta de eco, el comando **ping** proporciona comentarios acerca del tiempo transcurrido entre el envío de la solicitud y la recepción de la respuesta. Esto puede ser una medida del rendimiento de la red.

El comando ping tiene un valor de tiempo de espera para la respuesta. Si no se recibe una respuesta dentro del tiempo de espera, el comando ping proporciona un mensaje que indica que no se recibió una respuesta. Esto puede indicar que hay un problema, pero también podría indicar que las funciones de seguridad que bloquean los mensajes de ping se han habilitado en la red. Es común que el primer ping se agote si es necesario realizar la resolución de direcciones (ARP o ND) antes de enviar la solicitud de eco ICMP.

Una vez que se envían todas las solicitudes, la utilidad **ping** proporciona un resumen que incluye la tasa de éxito y el tiempo promedio del viaje de ida y vuelta al destino.

Los tipos de pruebas de conectividad que se realizan con **ping** son los siguientes:

* Hacer ping al loopback local
* Hacer ping a la puerta de enlace predeterminada
* Hacer ping al host remoto

### Loopback

Ping se puede usar para probar la configuración interna de IPv4 o IPv6 en el host local. Para realizar esta prueba, se debe hacer **ping** a la dirección de loopback local 127.0.0.1 para IPv4 (::1 para IPv6).

Una respuesta de 127.0.0.1 para IPv4 (o ::1 para IPv6) indica que IP está instalado correctamente en el host. Esta respuesta proviene de la capa de red. Sin embargo, esta respuesta no indica que las direcciones, las máscaras o los gateways estén configurados adecuadamente. Tampoco indica nada acerca del estado de la capa inferior de la pila de red. Simplemente, prueba el protocolo IP en la capa de red de dicho protocolo. Un mensaje de error indica que TCP/IP no funciona en el host.

* Hacer ping al host local permite confirmar que el protocolo TCP/IP se encuentra instalado en el host y que funciona.
* Hacer ping a 127.0.0.1 ocasiona que un dispositivo se haga ping a sí mismo.

### Puerta de Enlace Predeterminada

También es posible utilizar el comando **ping** para probar la capacidad de comunicación de un host en la red local. Esto generalmente se hace haciendo ping a la dirección IP de la puerta de enlace predeterminada del host. Un **ping** exitoso a la puerta de enlace predeterminada indica que el host y la interfaz del enrutador que sirve como puerta de enlace predeterminada están operando en la red local.

Para esta prueba, la dirección de puerta de enlace predeterminada se usa con mayor frecuencia porque el router normalmente siempre está operativo. Si la dirección de puerta de enlace predeterminada no responde, se puede enviar un **ping** a la dirección IP de otro host en la red local que se sabe que está operativo.

Si la puerta de enlace predeterminada u otro host responde, entonces el host local puede comunicarse con éxito a través de la red local. Si la puerta de enlace predeterminada no responde pero otro host sí, esto podría indicar un problema con la interfaz del router que funciona como la puerta de enlace predeterminada.

Una posibilidad es que se haya configurado una dirección de puerta de enlace predeterminada incorrecta en el host. Otra posibilidad es que la interfaz del router puede estar en funcionamiento, pero se le ha aplicado seguridad, de manera que no procesa o responde solicitudes de ping.

El host hace ping a su puerta de enlace predeterminada, enviando una solicitud de eco ICMP. La puerta de enlace predeterminada envía una respuesta de eco confirmando la conectividad.

### Host Remoto

También se puede utilizar el comando ping para probar la capacidad de un host local para comunicarse en una interconexión de redes. El host local puede hacer ping a un host IPv4 operativo de una red remota, como se muestra en la ilustración. El router utiliza su tabla de enrutamiento IP para reenviar los paquetes.

Si este ping se realiza correctamente, se puede verificar el funcionamiento de una amplia porción de la interconexión de redes. Un **ping** exitoso a través de la red confirma la comunicación en la red local, el funcionamiento del enrutador que sirve como puerta de enlace predeterminada y el funcionamiento de todos los demás enrutadores que podrían estar en la ruta entre la red local y la red del host remoto.

Además, se puede verificar la funcionalidad del host remoto. Si el host remoto no pudiera comunicarse fuera de su red local, no habría respondido.

### Traceroute

El comando ping se usa para probar la conectividad entre dos hosts, pero no proporciona información sobre los detalles de los dispositivos entre los hosts. Traceroute (**tracert**) es una utilidad que genera una lista de saltos que se alcanzaron correctamente a lo largo de la ruta. Esta lista puede proporcionar información importante sobre la verificación y la solución de problemas. Si los datos llegan al destino, el rastreo indica la interfaz de cada router que aparece en la ruta entre los hosts. Si los datos fallan en algún salto a lo largo del camino, la dirección del último router que respondió al rastreo puede indicar dónde se encuentra el problema o las restricciones de seguridad.

**Tiempo de Ida y Vuelta (RTT)**

El uso de traceroute proporciona tiempo de ida y vuelta para cada salto a lo largo del camino e indica si un salto no responde. El tiempo de ida y vuelta es el tiempo que tarda un paquete en llegar al host remoto y que la respuesta del host regrese. Se utiliza un asterisco (\*) para indicar un paquete perdido o sin respuesta.

Esta información se puede usar para localizar un router problemático en la ruta o puede indicar que el router está configurado para no responder. Si en la pantalla se muestran tiempos de respuesta elevados o pérdidas de datos de un salto en particular, esto constituye un indicio de que los recursos del router o sus conexiones pueden estar sobrecargados.

**TTL de IPv4 y Límite de Saltos de IPv6**

Traceroute utiliza una función del campo TTL en IPv4 y el campo Límite de Salto en IPv6 en los encabezados de Capa 3, junto con el mensaje de ICMP Tiempo Excedido.



### Referencias

{% embed url="https://skillsforall.com/course/networking-devices-and-initial-configuration?courseLang=en-US" %}

{% embed url="https://www.cisco.com/c/es_mx/support/docs/ios-nx-os-software/ios-software-releases-121-mainline/12778-ping-traceroute.html" %}
