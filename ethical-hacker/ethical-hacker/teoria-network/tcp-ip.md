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

# TCP/IP

Es un conjunto de reglas que permite el intercambio o transportes de datos,generalmente el protocolo en distintos niveles de capas:

| Capas                       | Protocolos             |
| --------------------------- | ---------------------- |
| Capa de aplicación          | aplicaciones           |
| Capa de transporte          | UDP Y TCP              |
| Capa de redes               | Protocolos de internet |
| Capa de interfaces de redes | interfaz de red        |
| Hardware                    | Red física             |

Los programas de aplicación envían mensajes o corrientes de datos a uno de los protocolos de la capa de transporte de Internet, UDP (User Datagram Protocol) o TCP (Transmission Control Protocolo). Estos protocolos reciben los datos de la aplicación, los dividen en partes más pequeñas llamadas _paquetes_, añaden una dirección de destino y, a continuación, pasan los paquetes a la siguiente capa de protocolo, la capa de red de Internet.

La capa de red de Internet pone el paquete en un datagrama de IP (Internet Protocol), pone la cabecera y la cola de datagrama, decide dónde enviar el datagrama (directamente a un destino o a una pasarela) y pasa el datagrama a la capa de interfaz de red.

La capa de interfaz de red acepta los datagramas IP y los transmite como _tramas_ a través de un hardware de red específico, por ejemplo redes Ethernet o de Red en anillo.

Las tramas recibidas por un sistema principal pasan a través de las capas de protocolo en sentido inverso. Cada capa quita la información de cabecera correspondiente, hasta que los datos regresan a la capa de aplicación.

La capa de interfaz de red (en este caso, un adaptador Ethernet) recibe las tramas. La capa de interfaz de red quita la cabecera Ethernet y envía el datagrama hacia arriba hasta la capa de red. En la capa de red, Protocolo Internet quita la cabecera IP y envía el paquete hacia arriba hasta la capa de transporte. En la capa de transporte, TCP (en este caso) quita la cabecera TCP y envía los datos hacia arriba hasta la capa de aplicación.

Los sistemas principales de una red envían y reciben información simultáneamente.



#### Referencias

{% embed url="https://skillsforall.com/course/networking-devices-and-initial-configuration?courseLang=en-US" %}
