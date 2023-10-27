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

A esta técnica se la conoce habitualmente como sondeo medio abierto, porque no se llega a abrir una conexión TCP completa. Se envía un paquete SYN, como si se fuera a abrir una conexión real y después se espera una respuesta.

```
nmap -sS 192.168.1.251
```

#### TCP Connect Scan (**-sT**)

Un escaneo de conexión TCP utiliza el mecanismo de red del sistema operativo subyacente para establecer una conexión TCP completa con el dispositivo de destino que se está escaneando. Debido a que crea una conexión completa, genera más tráfico y es mas lento. Este es el tipo de escaneo predeterminado que se utiliza si no se especifica ningún tipo de escaneo con el comando nmap. Sin embargo, normalmente solo debe utilizarse cuando un escaneo SYN no es una opción.

El sondeo TCP Connect() es el sondeo TCP por omisión cuando no se puede utilizar el sondeo SYN. Esto sucede, por ejemplo, cuando el usuario no tiene privilegios para enviar paquetes en crudo o cuando se están sondeando redes IPv6. Nmap le pide al sistema operativo subyacente que establezcan una conexión con el sistema objetivo en el puerto indicado utilizando la llamada del sistema `connect()`

Esto significa que se tarda más tiempo y son necesarios más paquetes para obtener la información, pero también significa que los sistemas objetivos van a registrar probablemente la conexión. Un administrador que vea muchos intentos de conexión en sus registros que provengan de un único sistema debería saber que ha sido sondeado con este método.

```
nmap -sT 192.168.1.251
```

#### UDP Scan (**-sU**)

Para realizar un escáner de UDP se utiliza `-sU` si estás intentando enumerar un servidor DNS, SNMP o DHCP. Todos estos servicios utilizan UDP para la comunicación entre el cliente y el servidor.

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

#### --exclude/excludefile

Estas opciones son útiles cuando quieres evitar escanear objetivos específicos, como servidores de misión crítica o subredes administradas por otras personas.

<pre><code><strong>nmap --exclude 192.168.1.100,192.168.1.0/24
</strong></code></pre>

#### Resolución de DNS `-n/-R`

Las opciones `-n` y `-R` de Nmap controlan la resolución de nombres durante un escaneo. La opción `-n` desactiva la resolución de nombres ya que DNS es generalmente lento, esto acelera un poco las cosas, mientras que la opción `-R` la activa para todos los objetivos.

La resolución de nombres es el proceso de traducir una dirección IP en un nombre de host. Nmap utiliza la resolución de nombres para identificar los nombres de host de los objetivos que encuentra.

```
nmap -sS -n 192.168.1.251
```

```
nmap -sS -R 192.168.1.251
```

#### Sondeo de lista `-sL`

El sondeo de lista es un tipo de descubrimiento de sistemas que simplemente enumera todos los equipos de la red especificada, sin enviar paquetes de ningún tipo a los objetivos.

La opción `-sL` de Nmap permite realizar un sondeo de lista. Esta opción no tiene argumentos.

```
nmap -sL 192.168.1.251
```

#### Sondeo especifico `-p`

La opción `-p` de Nmap especifica los puertos que deseas sondear. Puedes especificar tanto números de puerto de forma individual, como rangos de puertos separados por un guión. Puedes omitir el valor inicial y/o el valor final del rango. Nmap utilizará 1 ó 65535 respectivamente. De esta forma, puedes especificar `-p-` para sondear todos los puertos desde el 1 al 65535. Se permite sondear el puerto cero siempre que lo especifiques explícitamente.

```
nmap -p 80,443,22 192.168.1.251
```

o&#x20;

```
nmap -p- 192.168.1.251
```

#### Detección de versiones `-sV`

Activa la detección de versiones como se ha descrito previamente. Puede utilizar la opción `-A` en su lugar para activar tanto la detección de versiones como la detección de sistema operativo.

#### &#x20;No excluir ningún puerto de la detección de versiones `--allports`

La detección de versiones de Nmap omite el puerto TCP 9100 por omisión porque algunas impresoras imprimen cualquier cosa que reciben en este puerto, lo que da lugar a la impresión de múltiples páginas con solicitudes HTTP get, intentos de conexión de SSL, etc. Este comportamiento puede cambiarse modificando o eliminando la directiva `Exclude` en `nmap-service-probes`, o especificando `--allports` para sondear todos los puertos independientemente de lo definido en la directiva `Exclude`.

#### Modo ligero `--version-light`&#x20;

Éste es un alias conveniente para `--version-intensity 2`. Este modo ligero hace que la detección de versiones sea más rápida pero también hace que sea menos probable identificar algunos servicios.

#### Utilizar todas las sondas `--version-all`&#x20;

Éste es un alias para `--version-intensity 9`, hace que se utilicen todas las sondas contra cada puerto.

#### Detección de sistema operativo `-O`&#x20;

Tal y como se indica previamente, activa la detección de sistema operativo. También se puede utilizar la opción `-A` para activar la detección de sistema operativo y de versiones.

#### Incrementa el nivel de detalle `-v`&#x20;

Hace que Nmap imprima más información sobre el sondeo que está realizando incrementando el nivel de detalle. Los puertos abiertos se muestran en cuanto se encuentran y se muestra una estimación del tiempo que Nmap espera que dure la tarea de sondeo si piensa que va a durar más de un par de minutos. Puede utilizarlo dos veces para obtener aún más detalle. No tiene ningún efecto el utilizarlo más de dos veces.

#### Salida grepeable `-oG`&#x20;

Este formato de salida se trata el último porque está obsoleto. La salida en formato XML es mucho más poderosa, y es igual de conveniente para los usuarios experimentados. XML es un estándar para el que se dispone de docenas de intérpretes, mientras que la salida para grep es un «hack» propio. XML puede extenderse para soportar nuevas funcionalidades de Nmap tan pronto como se liberen, mientras que en general tengo que omitir estas funcionalidades de la salida para grep por no tener un lugar donde ponerlas.

#### Salida XML  `-oX`&#x20;

Solicita que la `salida en XML` se redirigida al archivo especificado.&#x20;

#### Salida normal `-oN`&#x20;

Solicita que la `salida normal` sea redirigida al archivo especificado. Como se ha dicho anteriormente.

`-6` (Activa el sondeo IPv6)

Nmap tiene soporte IPv6 para la mayoría de sus funcionalidades más populares desde 2002. En particular, tiene soporte de: sondeo ping (TCP-only), sondeo connect() y detección de versiones. La sintaxis de las órdenes es igual que las habituales salvo que debe especificar la opción `-6` Por supuesto, debe utilizarse la sintaxis IPv6 si se indica una dirección en lugar de un nombre de sistema. Una dirección IPv6 sería parecida a `3ffe:7501:4819:2000:210:f3ff:fe03:14d0`, por lo que se recomienda utilizar nombres de equipo. La salida es igual que en los otros casos. Lo único que distingue que esta opción está habilitada es que se muestran las direcciones IPv6 en la línea que indica los “puertos de interés”.

Aunque IPv6 no se está utilizando en todo el mundo, sí que se utiliza mucho en algunos países (generalmente asiáticos) y muchos sistemas operativos modernos lo soportan. Tanto el origen como el objetivo de su sondeo deben estar configurados para utilizar IPv6 si desea utilizar Nmap con IPv6. Si su ISP (como sucede con la mayoría) no le da direcciones IPv6, puede encontrar gestores de túneles gratuitos en muchos sitios y funciona bien con Nmap. Una lista de gestores está [en Wikipedia](http://es.wikipedia.org/wiki/Anexo:Proveedores\_de\_t%C3%BAneles\_IPv6). Los túneles IPv6 a IPv4 («6to4») son también otro método muy popular y gratuito.

`-A` (Opciones de sondeos agresivos)

Esta opción activa algunas opciones avanzadas y agresivas. Aún no he decidido qué significa exactamente. Actualmente esto activa la detección de sistema operativo (`-O`) y el análisis de versiones (`-sV`). Aunque se añadirán más opciones en el futuro. La idea es que esta opción active un conjunto de opciones para evitar que los usuarios de Nmap tengan que recordar un número de opciones muy elevado. Esta opción sólo activa funcionalidades, no afecta a las opciones de temporización (como `-T4`) o de depuración (`-v`) que quizás desee activar también.
