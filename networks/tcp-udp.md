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

# TCP/UDP

son los protocolos básicos de nivel de transporte para realizar conexiones entre sistemas principales de Internet. **TCP** y **UDP** permiten que los programas envíen mensajes a las aplicaciones de otros sistemas principales y reciban mensajes de dichas aplicaciones. Cuando una aplicación envía a la capa de transporte una petición de envío de un mensaje, **UDP** y **TCP** dividen la información en paquetes, añaden una cabecera de paquete incluida la dirección de destino y envían la información a la capa de red para su proceso adicional. **TCP** y **UDP** utilizan puertos de protocolo en el sistema principal para identificar el destino específico del mensaje.

El **UDP** proporciona un medio de datagrama de comunicación entre aplicaciones de sistemas principales de Internet.

Dado que los remitentes no saben qué procesos están activos en un momento determinado, **UDP** utiliza los puertos de protocolo de destino (o puntos de destino abstractos en una máquina), identificados por enteros positivos, para enviar mensaje a uno de los múltiples destinos de un sistema principal. Los puertos de protocolo reciben y conservan los mensajes en las colas hasta que las aplicaciones de la red de recepción puede recuperarlos.

Puesto que **UDP** se basa en el **IP** subyacente para enviar los datagramas, **UDP** proporciona la misma entrega de mensaje sin conexión que **IP**. No ofrece ninguna garantía de entrega de datagrama o de protección de duplicación. Sin embargo, **UDP** permite al remitente especificar números de puerto de origen y destino para el mensaje y calcula la suma de comprobación de los datos y la cabecera. Estos dos características permiten a las aplicaciones de envío y recepción asegurar la entrega correcta de un mensaje.
