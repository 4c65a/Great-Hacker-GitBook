# TCP/UDP Port Scanning

**El escaneo de puertos** es el proceso de identificar qué puertos están abiertos en una máquina remota. Esta información se puede utilizar para determinar qué servicios se están ejecutando en el objetivo e identificar posibles vectores de ataque.

**Notas importantes:**

* El escaneo de puertos no es representativo de la actividad típica del usuario y puede considerarse ilegal en algunas jurisdicciones. Siempre obtenga el permiso por escrito del propietario de la red antes de realizar escaneos de puertos.
* Es fundamental comprender las implicaciones del escaneo de puertos, así como el impacto que pueden tener los escaneos de puertos específicos. Debido a la cantidad de tráfico que pueden generar algunos escaneos, junto con su naturaleza intrusiva, ejecutar escaneos de puertos a ciegas puede tener efectos adversos en los sistemas objetivo o en la red del cliente, como la sobrecarga de servidores y enlaces de red o la activación de un IDS/IPS. Realizar el escaneo incorrecto podría resultar en tiempo de inactividad para el cliente.
* El uso de una metodología adecuada de escaneo de puertos puede mejorar significativamente nuestra eficiencia como testers de penetración al mismo tiempo que limita muchos de los riesgos. Dependiendo del alcance del compromiso, en lugar de realizar un escaneo completo de puertos contra la red objetivo, podemos comenzar escaneando solo los puertos 80 y 443. Con una lista de posibles servidores web, podemos ejecutar un escaneo completo de puertos contra estos servidores en segundo plano mientras realizamos otra enumeración. Una vez que se completa el escaneo completo del puerto, podemos refinar aún más nuestros escaneos para buscar más y más información con cada escaneo posterior.
* El escaneo de puertos debe entenderse como un proceso dinámico que es único para cada compromiso. Los resultados de un escaneo determinan el tipo y alcance del siguiente escaneo.

**Comenzaremos nuestra exploración del escaneo de puertos con un simple escaneo de puertos TCP y UDP usando Netcat.** Debe tenerse en cuenta que Netcat no es un escáner de puertos, pero se puede usar como tal de manera rudimentaria para mostrar cómo funciona un escáner de puertos típico.

**Sk y Dado que Netcat ya está presente en muchos sistemas, podemos reutilizar algunas de sus funciones para imitar un escaneo de puertos básico cuando no necesitemos un escáner de puertos con todas las funciones. También exploraremos herramientas dedicadas al escaneo de puertos en detalle.**

**Empecemos por cubrir las técnicas de escaneo TCP, centrándonos en UDP más adelante.** La técnica de escaneo de puertos TCP más simple, generalmente llamada escaneo CONNECT, se basa en el mecanismo de protocolo de enlace TCP de tres vías. Este mecanismo está diseñado para que dos hosts que intentan comunicarse puedan negociar los parámetros de la conexión de socket TCP de red antes de transmitir cualquier dato.

**En términos básicos, un host envía un paquete TCP SYN a un servidor en un puerto de destino. Si el puerto de destino está abierto, el servidor responde con un paquete SYN-ACK y el host cliente envía un paquete ACK para completar el protocolo de enlace. Si el protocolo de enlace se completa con éxito, el puerto se considera abierto.**

**Podemos demostrar esto ejecutando un escaneo de puerto TCP Netcat en los puertos 3388-3390.** Usaremos la opción -w para especificar el tiempo de espera de la conexión en segundos, así como -z para especificar el modo de E/S cero, que se utiliza para escanear y no envía datos.

```
kali@kali:~$ nc -nvv -w 1 -z 192.168.50.152 3388-3390
(DESCONOCIDO) [192.168.50.152] 3390 (?) : Conexión rechazada
(DESCONOCIDO) [192.168.50.152] 3389 (ms-wbt-server) abierto
(DESCONOCIDO) [192.168.50.152] 3388 (?) : Conexión rechazada
enviado 0, recibido 0
```

**Con base en esta salida, sabemos que el puerto 3389 está abierto, mientras que las conexiones en los puertos 3388 y 3390 han sido rechazadas.** La siguiente captura de pantalla muestra la captura de Wireshark de este escaneo.

**Sk y Ahora que tenemos una buena comprensión del protocolo de enlace TCP y hemos examinado cómo funciona un escaneo TCP en el fondo, cubramos el escaneo UDP.** Dado que UDP es sin estado y no implica un protocolo de enlace de tres
