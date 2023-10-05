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



### Unidifusión

En el tema anterior, aprendió acerca de la estructura de una dirección IPv4; cada una tiene una parte de red y una parte de host. Existen diferentes formas de enviar un paquete desde un dispositivo de origen, y estas diferentes transmisiones afectan a las direcciones IPv4 de destino.

La transmisión unidifusión se refiere a un dispositivo que envía un mensaje a otro dispositivo en comunicaciones uno a uno.

Un paquete de unidifusión tiene una dirección IP de destino que es una dirección de unidifusión que va a un único destinatario. Una dirección IP de origen sólo puede ser una dirección de unidifusión, ya que el paquete sólo puede originarse de un único origen. Esto es independiente de si la dirección IP de destino es una unidifusión, difusión o multidifusión.

### Difusión

Transmisión de transmisión hace referencia a un dispositivo que envía un mensaje a todos los dispositivos de una red en comunicaciones unipersonales.

Los paquetes de difusión tienen una dirección IPv4 de destino que contiene solo números uno (1) en la porción de host.

Todos los dispositivos del mismo dominio de difusión deben procesar un paquete de difusión. Un dominio de difusión identifica todos los hosts del mismo segmento de red. Una transmisión puede ser dirigida o limitada. Una difusión dirigida se envía a todos los hosts de una red específica. Por ejemplo, un host de la red 172.16.4.0/24 envía un paquete a la dirección 172.16.4.255. Se envía una difusión limitada a 255.255.255.255. De manera predeterminada, los enrutadores no reenvían difusiones.

Los paquetes de difusión usan recursos en la red y hacen que cada host receptor en la red procese el paquete. Por lo tanto, se debe limitar el tráfico de difusión para que no afecte negativamente el rendimiento de la red o de los dispositivos. Debido a que los enrutadores separan los dominios de difusión, la subdivisión de redes puede mejorar el rendimiento de la red al eliminar el exceso de tráfico de difusión.



### Multidifusión

La transmisión de multidifusión reduce el tráfico al permitir que un host envíe un único paquete a un grupo seleccionado de hosts que estén suscritos a un grupo de multidifusión.

Un paquete de multidifusión es un paquete con una dirección IP de destino que es una dirección de multidifusión. IPv4 reservó las direcciones de 224.0.0.0 a 239.255.255.255 como rango de multidifusión.

Los hosts que reciben paquetes de multidifusión particulares se denominan clientes de multidifusión. Los clientes de multidifusión utilizan servicios solicitados por un programa cliente para subscribirse al grupo de multidifusión.

Cada grupo de multidifusión está representado por una sola dirección IPv4 de destino de multidifusión. Cuando un host IPv4 se suscribe a un grupo de multidifusión, el host procesa los paquetes dirigidos a esta dirección de multidifusión y los paquetes dirigidos a la dirección de unidifusión asignada exclusivamente.

Los protocolos de enrutamiento como OSPF utilizan transmisiones de multidifusión. Por ejemplo, los routeres habilitados con OSPF se comunican entre sí mediante la dirección de multidifusión OSPF reservada 224.0.0.5. Sólo los dispositivos habilitados con OSPF procesarán estos paquetes con 224.0.0.5 como dirección IPv4 de destino. Todos los demás dispositivos ignorarán estos paquetes.

### Direcciones IPv4 Públicas y Privadas

Del mismo modo que hay diferentes formas de transmitir un paquete IPv4, también hay diferentes tipos de direcciones IPv4. Algunas direcciones IPv4 no se pueden usar para salir a Internet, y otras se asignan específicamente para enrutar a Internet. Algunos se utilizan para verificar una conexión y otros se autoasignan. Como administrador de red, eventualmente se familiarizará con los tipos de direcciones IPv4, pero por ahora, al menos debe saber qué son y cuándo usarlas.

Las direcciones IPv4 públicas son direcciones que se enrutan globalmente entre routeres de proveedores de servicios de Internet (ISP). Sin embargo, no todas las direcciones IPv4 disponibles pueden usarse en Internet. Existen bloques de direcciones denominadas direcciones privadas que la mayoría de las organizaciones usan para asignar direcciones IPv4 a los hosts internos.

A mediados de la década de 1990, con la introducción de la World Wide Web (WWW), se introdujeron direcciones IPv4 privadas debido al agotamiento del espacio de direcciones IPv4. Las direcciones IPv4 privadas no son exclusivas y cualquier red interna puede usarlas.

{% code fullWidth="true" %}
```

Rango de direcciones	        Tipo de dirección
0.0.0.0 a 0.255.255.255	        Privado
10.0.0.0 a 10.255.255.255	Privado
172.16.0.0 a 172.31.255.255	Privado
192.168.0.0 a 192.168.255.255	Privado
169.254.0.0 a 169.254.255.255	Auto-configuración de direcciones IP
Todo lo demás	                Público
```
{% endcode %}

### Direcciones IPv4 de uso especial

Existen ciertas direcciones, como la dirección de red y la dirección de difusión, que no se pueden asignar a los hosts. También hay direcciones especiales que pueden asignarse a los hosts, pero con restricciones respecto de la forma en que dichos hosts pueden interactuar dentro de la red.

**Direcciones de loopback**

Las direcciones de bucle invertido (loopback) (127.0.0.0 /8 o 127.0.0.1 a 127.255.255.254) se identifican más comúnmente como solo 127.0.0.1. Estas son direcciones especiales utilizadas por un host para dirigir el tráfico hacia sí mismo. Por ejemplo, el comando **ping** se usa comúnmente para probar conexiones a otros hosts.

**Direcciones de enlace local**

Direcciones link-local o direcciones IP privadas automáticas (APIPA) 169.254.0.0/16o 169.254.0.1 a 169.254.255.254 Los utiliza un cliente de Windows para auto configurarse en caso de que el cliente no pueda obtener un direccionamiento IP a través de otros métodos. Las direcciones locales de vínculo se pueden utilizar en una conexión de punto a punto, pero no se utilizan comúnmente para este propósito.

### Ipv6

> NAT, o Network Address Translation, es un mecanismo que permite a dispositivos con direcciones IP privadas comunicarse con dispositivos con direcciones IP públicas.

IPv6 está diseñado para ser el sucesor de IPv4. IPv6 tiene un espacio de direcciones más grande de 128 bits, que proporciona 340 undecillones (es decir, 340 seguidos de 36 ceros) posibles direcciones. Sin embargo, IPv6 es más que solo direcciones más extensas.

Cuando el IETF comenzó a desarrollar un sucesor de IPv4, aprovechó esta oportunidad para corregir las limitaciones de IPv4 e incluir mejoras. Un ejemplo es el Protocolo de mensajes de control de Internet versión 6 (ICMPv6), que incluye la resolución de direcciones y la configuración automática de direcciones que no se encuentran en ICMP para IPv4 (ICMPv4).

El agotamiento del espacio de direcciones IPv4 fue el factor que motivó la migración a IPv6. A medida que África, Asia y otras áreas del mundo están más conectadas a Internet, no hay suficientes direcciones IPv4 para acomodar este crecimiento. Como se muestra en la ilustración, a cuatro de cinco Registros Regionales de Internet (RIR) se les agotaron las direcciones IPv4.

### Las técnicas de migración de IPv4 a IPv6

#### Doble Pila/Dual stack

Doble pila permite que IPv4 e IPv6 coexistan en el mismo segmento de red. Los dispositivos dual-stack ejecutan pilas de protocolos IPv4 e IPv6 de manera simultánea.

#### Tunelización

La tunelización es un método para transportar un paquete IPv6 a través de una red IPv4. El paquete IPv6 se encapsula dentro de un paquete IPv4.

#### Traducción

La Traducción de Direcciones de Redes 64 (NAT64) permite que los dispositivos con IPv6 habilitado se comuniquen con dispositivos con IPv4 habilitado mediante una técnica de traducción similar a la NAT para IPv4.
