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

### Servicios y puertos

Accedemos a gran cantidad de servicios a través de internet durante el día.Cuando se entrega un mensaje mediante TCP o UDP, los protocolos y servicios solicitados se identifican mediante un número de puerto. Un puerto es un identificador numérico dentro de cada segmento, que se usa para llevar un seguimiento de las conversaciones específicas entre un cliente y un servidor. Cada mensaje que envía un host contiene un puerto de origen y un puerto de destino.

Entre los dos protocolos cubre varios puertos y estos son los mas conocidos:

<table data-header-hidden><thead><tr><th>Servicios</th><th>TCP/UDP</th><th>Puertos</th><th data-hidden data-type="number"></th></tr></thead><tbody><tr><td>SSH</td><td>TCP</td><td>22</td><td>null</td></tr><tr><td>FTP</td><td>TCP</td><td>20, 21</td><td>null</td></tr><tr><td>DNS</td><td>UDP</td><td>53</td><td>null</td></tr><tr><td>DHCP</td><td>UDP</td><td>67, 68</td><td>null</td></tr><tr><td>SNMP</td><td>UDP</td><td>161, 162</td><td>null</td></tr><tr><td>IMAP</td><td>TCP</td><td>143</td><td>null</td></tr><tr><td>HTTPS</td><td>TCP</td><td>443</td><td>null</td></tr><tr><td>MySql</td><td>TCP</td><td>3306</td><td>null</td></tr><tr><td>HTTP</td><td>TCP</td><td>80</td><td>null</td></tr><tr><td>SNMP</td><td>UDP</td><td>161</td><td>null</td></tr><tr><td>Telnet</td><td>TCP</td><td>23</td><td>null</td></tr></tbody></table>
