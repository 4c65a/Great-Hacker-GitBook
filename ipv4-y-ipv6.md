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

# IPv4 y IPv6

### La Dirección IPv4

Un host necesita una dirección IPv4 para participar en Internet y en casi todas las LAN hoy en día. La dirección IPv4 es una dirección de red lógica que identifica a un host en particular Debe configurarse correctamente y ser única dentro de la red LAN, para posibilitar la comunicación local. También debe configurarse correctamente y ser única en el mundo, para posibilitar la comunicación remota. Así es como un host puede comunicarse con otros dispositivos en Internet.

Se asigna una dirección IPv4 a la conexión de la interfaz de red para un host. Esta conexión generalmente es una tarjeta de interfaz de red (NIC) instalada en el dispositivo. Algunos ejemplos de dispositivos de usuario final con interfaces de red incluyen las estaciones de trabajo, los servidores, las impresoras de red y los teléfonos IP. Algunos servidores pueden tener más de una NIC, y cada una de ellas tiene su propia dirección IPv4. Las interfaces del enrutador que proporcionan conexiones a una red IP también tendrán una dirección IPv4.

Cada paquete que se envía por Internet tiene una dirección IPv4 de origen y de destino. Los dispositivos de red requieren esta información para asegurarse de que la información llegue a destino y de que toda respuesta sea devuelta al origen.

### Octetos y notación decimal con puntos

Las direcciones IPv4 tienen 32 bits de longitud. Aquí hay una dirección IPv4 en binario:\
**11010001101001011100100000000001**

Observe lo difícil que es leer esta dirección. ¡Imagine tener que configurar dispositivos con una serie de 32 bits! Por esta razón, los 32 bits se agrupan en cuatro bytes de 8 bits llamados octetos así:\
**11010001.10100101.11001000.00000001**

Eso está mejor, pero sigue siendo difícil de leer. Por ese motivo, cada octeto se representa como su valor decimal separado por un punto decimal. El IPv4 binario anterior se convierte en esta representación decimal con puntos:\
**209.165.200.1**
