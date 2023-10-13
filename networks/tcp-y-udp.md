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

# TCP y UDP

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

### Características TCP/UDP

<table><thead><tr><th width="356">TCP</th><th>UDP</th></tr></thead><tbody><tr><td><strong>Establece una sesión</strong></td><td><strong>Los datos se reconstruyen en el orden en que se recibieron</strong></td></tr><tr><td><strong>Garantiza una Entrega Confiable</strong></td><td><strong>Los segmentos perdidos no se vuelven a enviar</strong></td></tr><tr><td><strong>Proporciona Entrega en el Orden Correcto</strong></td><td><strong>No hay establecimiento de sesión</strong></td></tr><tr><td><strong>Admite Control de Flujo</strong></td><td><strong>El envío no está informado sobre la disponibilidad de recursos</strong></td></tr></tbody></table>

### Protocolo TCP de Enlace de Tres Vías

Los hosts mantienen el estado, rastrean cada segmento de datos dentro de una sesión e intercambian información sobre qué datos se reciben utilizando la información en el encabezado TCP. TCP es un protocolo full-duplex, donde cada conexión representa dos sesiones de comunicación unidireccionales. Para establecer la conexión, los hosts realizan un enlace de tres vías. Como se muestra en la figura, los bits de control en el encabezado TCP indican el progreso y el estado de la conexión.

Estas son las funciones del apretón de manos de tres vías:

* Establece que el dispositivo de destino está presente en la red.
* Verifica que el dispositivo de destino tenga un servicio activo y acepte solicitudes en el número de puerto de destino que el cliente de origen desea utilizar.
* Informa al dispositivo de destino que el cliente de origen intenta establecer una sesión de comunicación en dicho número de puerto.

Una vez que se completa la comunicación, se cierran las sesiones y se finaliza la conexión. Los mecanismos de conexión y sesión habilitan la función de confiabilidad de TCP.

Los seis bits del campo de bits de control del encabezado del segmento TCP también se conocen como marcadores. Una bandera es un bit que está activado o desactivado.

Los seis indicadores de bits de control son los siguientes:

* **URG** - Campo indicador urgente significativo
* **ACK**- Indicador de acuse de recibo utilizado en el establecimiento de la conexión y la terminación de la sesión
* **PSH** - Función de empuje
* **RST**- Restablece la conexión cuando se produce un error o un tiempo de espera
* **SYN**- Sincroniza números de secuencia utilizados en el establecimiento de conexión
* **FIN**- No más datos del remitente y se utilizan en la terminación de la sesión
