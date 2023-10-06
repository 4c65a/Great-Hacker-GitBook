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

Son los protocolos que realizar conexiones entre sistemas principales de Internet.Los dos protocolos permiten que los programas envíen mensajes a las aplicaciones de otros sistemas principales y reciban mensajes de dichas aplicaciones. Cuando una aplicación envía a la capa de transporte una petición de envío de un mensaje, **UDP** y **TCP** dividen la información en paquetes, añaden una cabecera de paquete incluida la dirección de destino y envían la información a la capa de red para su proceso adicional. **TCP** y **UDP** utilizan puertos de protocolo en el sistema principal para identificar el destino específico del mensaje.

El **UDP** proporciona un medio de datagrama de comunicación entre aplicaciones de sistemas principales de Internet.

Dado que los remitentes no saben qué procesos están activos en un momento determinado, **UDP** utiliza los puertos de protocolo de destino (o puntos de destino abstractos en una máquina), identificados por enteros positivos, para enviar mensaje a uno de los múltiples destinos de un sistema principal. Los puertos de protocolo reciben y conservan los mensajes en las colas hasta que las aplicaciones de la red de recepción puede recuperarlos.

> **TCP (Transmission Control Protocol)**: Un protocolo de transporte confiable que garantiza la entrega ordenada y sin errores de datos en una red.
>
>
>
> **UDP (User Datagram Protocol)**: Un protocolo de transporte más simple y sin conexión que se utiliza para la transmisión de datos en tiempo real.

