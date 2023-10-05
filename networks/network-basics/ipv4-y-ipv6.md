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

Se asigna una dirección IPv4 a la conexión de la interfaz de red para un host. Esta conexión generalmente es una tarjeta de interfaz de red (NIC) instalada en el dispositivo. Algunos servidores pueden tener más de una NIC, y cada una de ellas tiene su propia dirección IPv4.

Cada paquete que se envía por Internet tiene una dirección IPv4 de origen y de destino.

### Octetos y notación decimal con puntos

Las direcciones IPv4 tienen 32 bits de longitud. Aquí hay una dirección IPv4 en binario:\
**11010001101001011100100000000001**

Observe lo difícil que es leer esta dirección. ¡Imagine tener que configurar dispositivos con una serie de 32 bits! Por esta razón, los 32 bits se agrupan en cuatro bytes de 8 bits llamados octetos así:\
**11010001.10100101.11001000.00000001**

El IPv4 binario anterior se convierte en esta representación decimal con puntos:\
**209.165.200.1**

### Redes y Hosts

> **¿Que es un Host?**
>
> Cuando se habla de host se refiere a los distintos dispositivos ,con el host se puede indicar que nombre de hosts corresponde a una determinada dirección IP.
>
> **Ejemplo:**\
> Cuando realiza una maquina en <mark style="color:green;">HackTheBox</mark> generalmente deberá dirigirse al archivo /etc/host
>
> para poder avanzar con la maquina si es un sitio web deberá colocar en el archivo:\
> 10.11.0.251  snoopy.htb
>
> Ahora con eso podrás colocar snoopy.htb en el navegador y te cargara la misma pagina que antes te cargaba con la IP.

La dirección IPv4 lógica de 32 bits  consta de dos partes, la de red y la de host. Las dos partes se requieren en una dirección IPv4. Ambas redes tienen la máscara de sub red 255.255.255.0. La máscara de sub red se utiliza para identificar la red a la que está conectado el host.

A modo de ejemplo, hay un host con la dirección IPv4 192.168.5.11 y la máscara de sub red 255.255.255.0. Los primeros tres octetos (192.168.5), identifican la porción de red de la dirección, y el último octeto (11) identifica al host. Esto se conoce como direccionamiento jerárquico, debido a que la porción de red indica la red en la que cada dirección host única está ubicada. Los enrutadores solo necesitan conocer cómo llegar a cada red en lugar de conocer la ubicación de cada host individual.

Con el direccionamiento IPv4 pueden existir varias redes lógicas en una red física, si la porción de red de las direcciones del host correspondiente a la red es diferente.&#x20;

