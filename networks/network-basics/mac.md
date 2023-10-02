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

# MAC

Es el identificador único asignado por el fabricante a una pieza de hardware de red MAC significa Media Access Control.

Una dirección MAC consiste en seis grupos de dos caracteres, cada uno de ellos separado por dos puntos. 00:1B:44:11:3A:B7 ,Nos permite identificar a un ordenador/dispositivo sin importar la dirección IP.

***

### Switch y MAC

Un switch Ethernet es un dispositivo que se utiliza en la capa 2 OSI. Cuando un host envía un mensaje a otro host conectado a la misma red conmutada, el conmutador acepta y decodifica las tramas para leer la parte de la dirección MAC del mensaje. Una tabla en el switch, llamada tabla de direcciones MAC, contiene una lista de todos los puertos activos y las direcciones MAC del host que se adjuntan a ellos. Cuando se envía un mensaje entre hosts, el conmutador verifica si la dirección MAC de destino está en la tabla. Si está, el conmutador establece una conexión temporal, llamada circuito, entre el puerto de origen y el puerto de destino. Los conmutadores Ethernet también permiten enviar y recibir tramas a través del mismo cable Ethernet simultáneamente.&#x20;

Para crear la tabla de direcciones MAC, los conmutadores examinan la dirección MAC de origen de cada trama que se envía entre los hosts. Cuando un host envía un mensaje o responde a un mensaje enviado por inundación, el conmutador inmediatamente aprende la dirección MAC de ese host y el puerto al que está conectado. La tabla se actualiza de manera dinámica cada vez que el conmutador lee una nueva dirección MAC de origen.
