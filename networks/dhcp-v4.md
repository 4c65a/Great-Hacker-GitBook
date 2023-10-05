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

# DHCP/v4

El DHCP (**Dynamic Host Configuration Protocol**) es un protocolo de red que utiliza una arquitectura cliente-servidor. Este protocolo se encarga de asignar de manera dinámica y automática una dirección IP, ya sea una dirección IP privada desde el router hacia los equipos de la red local, o también una IP pública por parte de un operador que utilice este tipo de protocolo para el establecimiento de la conexión.

Varios tipos de dispositivos pueden actuar como servidores DHCP, siempre y cuando ejecuten software de servicios DHCP.

Muchas redes domésticas y de empresas pequeñas utilizan un enrutador inalámbrico y un módem. El enrutador inalámbrico actúa como cliente para recibir su configuración IPv4 del ISP y, luego, actúa como servidor DHCP para los hosts internos en la red local. El enrutador recibe la dirección IPv4 pública del ISP y, en su rol de servidor DHCP, distribuye direcciones privadas a los hosts internos.

El servidor DHCP está configurado con un rango  de direcciones IPv4 que pueden ser asignadas a clientes DHCP. El cliente que necesite una dirección IPv4 enviará un mensaje Descubrir DHCP (DHCP Discover), que es una difusión con dirección IPv4 de destino 255.255.255.255 (32 unos) y dirección MAC de destino FF-FF-FF-FF-FF-FF (48 unos). Todos los hosts de la red recibirán esta trama DHCP de difusión, pero solo un servidor DHCP responderá. El servidor responderá con una Oferta de DHCP (DHCP Offer) y sugerirá una dirección IPv4 para el cliente. Luego, el host envía una Solicitud DHCP (DHCP Request) a ese servidor, en la cual pedirá autorización para utilizar la dirección IPv4 sugerida. El servidor responde con una confirmación de recepción DHCP.

DHCPv4 utiliza cuatro tipos de mensajes para asignar direcciones IP y otros parámetros de configuración a los dispositivos conectados a una red IPv4.

**Mensaje DHCPDISCOVER**

El mensaje DHCPDISCOVER es enviado por un dispositivo que se conecta a una red IPv4 para solicitar una dirección IP y otros parámetros de configuración. El mensaje se envía como un broadcast, lo que significa que es recibido por todos los dispositivos en la red.

**Mensaje DHCPOFFER**

El mensaje DHCPOFFER es enviado por un servidor DHCP en respuesta a un mensaje DHCPDISCOVER. El mensaje contiene una oferta de una dirección IP y otros parámetros de configuración. El dispositivo que envió el mensaje DHCPDISCOVER puede aceptar o rechazar la oferta.

**Mensaje DHCPREQUEST**

El mensaje DHCPREQUEST es enviado por un dispositivo para aceptar una oferta de DHCPOFFER. El mensaje también puede utilizarse para solicitar una renovación de un arrendamiento existente.

**Mensaje DHCPACK**

El mensaje DHCPACK es enviado por un servidor DHCP en respuesta a un mensaje DHCPREQUEST. El mensaje confirma la asignación de la dirección IP y otros parámetros de configuración.



