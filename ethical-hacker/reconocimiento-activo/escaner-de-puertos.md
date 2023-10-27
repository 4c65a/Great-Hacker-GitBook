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

# Escáner de Puertos

## Escanear puerto con nmap

Un escaneo de puertos es un escaneo activo en el que la herramienta de escaneo envía varios tipos de sondas a la dirección IP de destino y luego examina las respuestas para determinar si el servicio está realmente escuchando. Nmap tiene varios comandos para hacer un escaneo exitoso.

**Se puede encontrar mas información en el sitio web:**

**Español:** [**https://nmap.org/man/es/**](https://nmap.org/man/es/)

**Ingles:** [**https://nmap.org**](https://nmap.org)

### Comandos

#### Scan SYN -sS

El parámetro `-sS` indica a Nmap que utilice un escaneo SYN. Este tipo de escaneo es el más común y se utiliza para identificar los puertos abiertos en un host sin establecer una conexión completa.&#x20;

Puede realizarse rápidamente, sondeando miles de puertos por segundo en una red rápida en la que no existan cortafuegos. El sondeo SYN es relativamente sigiloso y poco molesto, ya que no llega a completar las conexiones TCP. El escaneo muestra una clara y fiable diferenciación entre los estados `abierto`, `cerrado`, y `filtrado`.

A esta técnica se la conoce habitualmente como sondeo medio abierto, porque no se llega a abrir una conexión TCP completa. Se envía un paquete SYN, como si se fuera a abrir una conexión real y después se espera una respuesta. Si se recibe un paquete SYN/ACK esto indica que el puerto está en escucha (abierto), mientras que si se recibe un RST (reset) indica que no hay nada escuchando en el puerto. Si no se recibe ninguna respuesta después de realizar algunas retransmisiones entonces el puerto se marca como filtrado. También se marca el puerto como filtrado si se recibe un error de tipo ICMP no alcanzable (tipo 3, códigos 1,2, 3, 9, 10, ó 13).

```
nmap -sS 192.168.1.251
```

#### TCP Connect Scan (**-sT**)

Un escaneo de conexión TCP utiliza el mecanismo de red del sistema operativo subyacente para establecer una conexión TCP completa con el dispositivo de destino que se está escaneando. Debido a que crea una conexión completa, genera más tráfico (y, por lo tanto, tarda más tiempo en ejecutarse). Este es el tipo de escaneo predeterminado que se utiliza si no se especifica ningún tipo de escaneo con el comando nmap. Sin embargo, normalmente solo debe utilizarse cuando un escaneo SYN no es una opción.

El sondeo TCP Connect() es el sondeo TCP por omisión cuando no se puede utilizar el sondeo SYN. Esto sucede, por ejemplo, cuando el usuario no tiene privilegios para enviar paquetes en crudo o cuando se están sondeando redes IPv6. Nmap le pide al sistema operativo subyacente que establezcan una conexión con el sistema objetivo en el puerto indicado utilizando la llamada del sistema `connect()`

Nmap tiene menos control sobre la llamada de alto nivel `Connect()` que cuando utiliza paquetes en crudo, lo que hace que sea menos eficiente. La llamada al sistema completa las conexiones para abrir los puertos objetivo, en lugar de realizar el reseteo de la conexión medio abierta como hace el sondeo SYN. Esto significa que se tarda más tiempo y son necesarios más paquetes para obtener la información, pero también significa que los sistemas objetivos van a registrar probablemente la conexión. Un administrador que vea muchos intentos de conexión en sus registros que provengan de un único sistema debería saber que ha sido sondeado con este método.

```
nmap -sT 192.168.1.251
```

#### UDP Scan (**-sU**)

Aunque la mayoría de los servicios más habituales en Internet utilizan el protocolo TCP, los servicios [UDP](http://www.rfc-editor.org/rfc/rfc768.txt) también son muy comunes. Tres de los más comunes son los servicios DNS, SNMP, y DHCP (puertos registrados 53, 161/162, y 67/68 respectivamente). Dado que el sondeo UDP es generalmente más lento y más difícil que TCP, algunos auditores de seguridad ignoran estos puertos. Esto es un error, porque es muy frecuente encontrarse servicios UDP vulnerables y los atacantes no ignoran estos protocolos. Afortunadamente, Nmap puede utilizarse para hacer un inventario de puertos UDP.

El sondeo UDP se activa con la opción `-sU`. Puede combinarse con un tipo de sondeo TCP como el sondeo SYN (`-sS`) para comprobar ambos protocolos al mismo tiempo.

Los sondeo UDP funcionan mediante el envío (sin datos) de una cabecera UDP para cada puerto objetivo. Si se obtiene un error ICMP que indica que el puerto no es alcanzable (tipo 3, código 3) entonces se marca el puerto como `cerrado`. Si se recibe cualquier error ICMP no alcanzable (tipo 3, códigos 1, 2, 9, 10, o 13) se marca el puerto como `filtrado`. En algunas ocasiones se recibirá una respuesta al paquete UDP, lo que prueba que el puerto está `abierto`. Si no se ha recibido ninguna respuesta después de algunas retransmisiones entonces se clasifica el puerto como `abierto|filtrado`. Esto significa que el puerto podría estar abierto o que hay un filtro de paquetes bloqueando la comunicación. Puede utilizarse el sondeo de versión (`-sV`) para diferenciar de verdad los puertos abiertos de los filtrados.

Uno de las grandes problemas con el sondeo UDP es hacerlo rápidamente. Pocas veces llega una respuesta de un puerto abierto o filtrado, lo que obliga a expirar a Nmap y luego a retransmitir los paquetes en caso de que la sonda o la respuesta se perdieron. Los puertos cerrados son aún más comunes y son un problema mayor. Generalmente envían un error ICMP de puerto no alcanzable. Pero, a diferencia de los paquetes RST que envían los puertos TCP cerrados cuando responden a un sondeo SYN o Connect, muchos sistemas imponen una tasa máxima de mensajes ICMP de puerto inalcanzable por omisión. Linux y Solaris son muy estrictos con esto. Por ejemplo, el núcleo de Linux versión 2.4.20 limita la tasa de envío de mensajes de destino no alcanzable a uno por segundo (en `net/ipv4/icmp.c`).

Nmap detecta las limitaciones de tasa y se ralentiza para no inundar la red con paquetes inútiles que el equipo destino acabará descartando. Desafortunadamente, un límite como el que hace el núcleo de Linux de un paquete por segundo hace que un sondeo de 65536 puertos tarde más de 18 horas. Puede acelerar sus sondeo UDP incluyendo más de un sistema para sondearlos en paralelo, haciendo un sondeo rápido inicial de los puertos más comunes, sondeando detrás de un cortafuegos, o utilizando la opción `--host-timeout` para omitir los sistemas que respondan con lentitud.

```
nmap -sU 192.168.1.251
```

#### TCP FIN Scan (**-sF**)

```
nmap -sT 192.168.1.251
```

#### Host Discovery Scan (**-sn**)

```
nmap -sT 192.168.1.251
```

#### Timing Options (**-T 0-5**)

```
nmap -sT 192.168.1.251
```
