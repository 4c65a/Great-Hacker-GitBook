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

**TIP** Nmap scans only the 1000 most common ports for each protocol. You can specify additional ports to scan by using the -p option. You can obtain additional information about the port specifications and scan order from [_https://nmap.org/book/man-port-specification.html_](https://nmap.org/book/man-port-specification.html). Omar Santos has also created an Nmap Cheat Sheet that includes all options and is available in his GitHub repository, [_https://github.com/The-Art-of-Hacking/h4cker/blob/master/cheat\_sheets/NMAP\_cheat\_sheet.md_](https://github.com/The-Art-of-Hacking/h4cker/blob/master/cheat\_sheets/NMAP\_cheat\_sheet.md).

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

Para realizar un escáner de UDP se utiliza `-sU` si estás intentando enumerar un servidor DNS, SNMP o DHCP. Todos estos servicios utilizan UDP para la comunicación entre el cliente y el servidor.

Para escanear puertos UDP, Nmap envía un paquete UDP a todos los puertos especificados en la configuración de la línea de comandos. Espera una respuesta del objetivo. Si recibe un mensaje ICMP de puerto inalcanzable de un objetivo, ese puerto se marca como cerrado. Si no recibe respuesta del puerto UDP de destino, Nmap marca el puerto como abierto/filtrado. La siguiente tabla muestra las respuestas del escaneo UDP:

Dado que el sondeo UDP es generalmente más lento y más difícil que TCP, algunos auditores de seguridad ignoran estos puertos. Esto es un error, porque es muy frecuente encontrarse servicios UDP vulnerables y los atacantes no ignoran estos protocolos.

El sondeo UDP se activa con la opción `-sU`. Puede combinarse con un tipo de sondeo TCP como el sondeo SYN (`-sS`) para comprobar ambos protocolos al mismo tiempo.

```
nmap -sU -sS 192.168.88.251
```

Los sondeo UDP funcionan mediante el envío (sin datos) de una cabecera UDP para cada puerto objetivo. Si se obtiene un error ICMP que indica que el puerto no es alcanzable (tipo 3, código 3) entonces se marca el puerto como `cerrado`. Si se recibe cualquier error ICMP no alcanzable (tipo 3, códigos 1, 2, 9, 10, o 13) se marca el puerto como `filtrado`. En algunas ocasiones se recibirá una respuesta al paquete UDP, lo que prueba que el puerto está `abierto`. Si no se ha recibido ninguna respuesta después de algunas retransmisiones entonces se clasifica el puerto como `abierto|filtrado`. Esto significa que el puerto podría estar abierto o que hay un filtro de paquetes bloqueando la comunicación.&#x20;

```
nmap -sU 192.168.1.251
```

Consejo puede utilizarse el comando  (`-sV`) para diferenciar  los puertos abiertos de los filtrados.

```
nmap -sV 
```

#### TCP FIN Scan (**-sF**)

Un escaneo SYN puede ser captado por un filtro de red o un firewall. Se debe utilizar un tipo de paquete diferente en un escaneo de puertos. Con el escaneo FIN TCP, se envía un paquete FIN a un puerto de destino. Si el puerto está realmente cerrado, el sistema de destino envía un paquete RST. Si no se recibe nada del puerto de destino, puedes considerar que el puerto está abierto, ya que el comportamiento normal sería ignorar el paquete FIN.

```
nmap -sF 192.168.1.251
```

#### Host Discovery Scan (**-sn**)

Un escaneo de descubrimiento de hosts es uno de los tipos de escaneos más comunes utilizados para enumerar hosts en una red porque puede utilizar diferentes tipos de mensajes ICMP para determinar si un host está en línea y responde en una red.

```
nmap -sn 192.168.1.251
```

#### Timing Options (**-T 0-5**)

Nmap proporciona seis plantillas de temporización que se pueden especificar con la opción `-T`. Las plantillas de temporización de Nmap te permiten dictar cuán agresivo será un escaneo, mientras dejas que Nmap elija los valores de temporización exactos. Estas son las opciones de temporización:

* `-T0 (Paranoico)`: Muy lento, utilizado para evadir IDS.
* `-T1 (Sneaky)`: Bastante lento, utilizado para evadir IDS.
* `-T2 (Polite)`: Reduce la velocidad para consumir menos ancho de banda, se ejecuta aproximadamente 10 veces más lento que el predeterminado.
* `-T3 (Normal)`: Predeterminado, un modelo de temporización dinámico basado en la capacidad de respuesta del objetivo.
* `-T4 (Agresivo)`: Supone una red rápida y confiable y puede abrumar a los objetivos.
* `-T5 (Loco)`: Muy agresivo; probablemente abrumará a los objetivos o perderá puertos abiertos.

```
nmap -T0 192.168.1.251
```
