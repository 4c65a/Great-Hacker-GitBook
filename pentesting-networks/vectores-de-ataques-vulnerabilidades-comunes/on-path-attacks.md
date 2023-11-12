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

# On-Path Attacks

En un ataque en ruta (anteriormente conocido como ataque de hombre en el medio \[MITM]), un atacante se coloca en línea entre dos dispositivos o individuos que se comunican para espiar (es decir, robar datos confidenciales) o manipular los datos que se transfieren.

### **Suplantación de identidad de ARP y envenenamiento de caché de ARP**

El envenenamiento de la caché de ARP  es un ejemplo de un ataque que conduce a un escenario de ataque en ruta. Un ataque de suplantación de ARP puede tener como objetivo hosts, conmutadores y enrutadores conectados a una red de Capa 2 envenenando las cachés ARP de los sistemas conectados a la subred e interceptando el tráfico destinado a otros hosts en la subred.&#x20;

El atacante falsifica las direcciones MAC de Capa 2 para hacer creer a la víctima que la dirección de Capa 2 del atacante es la dirección de Capa 2 de su puerta de enlace predeterminada (10.2.3.4). Los paquetes que se supone deben ir a la puerta de enlace predeterminada son reenviados por el conmutador a la dirección de Capa 2 del atacante en la misma red. El atacante puede reenviar los paquetes IP al destino correcto para permitir que el cliente acceda al servidor web (10.2.66.77).

_**La suplantación de control de acceso a medios (MAC)**_ es un ataque en el que un actor de amenazas se hace pasar por la dirección MAC de otro dispositivo (normalmente un dispositivo de infraestructura como un enrutador). La dirección MAC suele ser una dirección codificada en un controlador de interfaz de red. En entornos virtuales, la dirección MAC podría ser una dirección virtual (es decir, no asignada a un adaptador físico). Un atacante podría falsificar la dirección MAC de sistemas físicos o virtuales para eludir las medidas de control de acceso o realizar un ataque en ruta.

Una mitigación común para los ataques de envenenamiento de caché ARP es utilizar la inspección del Protocolo de resolución de direcciones dinámicas (ARP) (DAI) en los conmutadores para evitar la suplantación de direcciones de capa 2.

Otro ataque en ruta de Capa 2 implica colocar un conmutador en la red y manipular el protocolo de árbol de expansión (STP) para convertirlo en el conmutador raíz. Este tipo de ataque puede permitir a un atacante ver cualquier tráfico que deba enviarse a través del conmutador raíz.

Un atacante puede llevar a cabo un ataque en ruta en la Capa 3 colocando un enrutador no autorizado en la red y luego engañando a los otros enrutadores haciéndoles creer que este nuevo enrutador tiene una ruta mejor que otros enrutadores. También es posible realizar un ataque en ruta comprometiendo el sistema de la víctima e instalando malware que pueda interceptar los paquetes enviados por la víctima. El malware puede capturar paquetes antes de cifrarlos si la víctima utiliza SSL/TLS/HTTPS o cualquier otro mecanismo. Una herramienta de ataque llamada SSLStrip utiliza la funcionalidad en ruta para observar de forma transparente el tráfico HTTPS, secuestrar y devolver enlaces HTTP no cifrados al usuario como respuesta.&#x20;

Las siguientes son algunas prácticas recomendadas de seguridad de Capa 2 adicionales para proteger su infraestructura:

* Seleccione una VLAN no utilizada (que no sea la VLAN 1) y úsela como VLAN nativa para todas sus troncales. No utilice esta VLAN nativa para ninguno de sus puertos de acceso habilitados. Evite usar VLAN 1 en cualquier lugar porque es la opción predeterminada.
* Configurar administrativamente los puertos del switch como puertos de acceso para que los usuarios no puedan negociar una troncal; También deshabilite la negociación de enlace troncal (es decir, no permita el protocolo de enlace troncal dinámico \[DTP]).
* Limite la cantidad de direcciones MAC aprendidas en un puerto determinado mediante la función de seguridad del puerto.
* Controle Spanning Tree para evitar que usuarios o dispositivos desconocidos lo manipulen. Puede hacerlo utilizando las funciones BPDU Guard y Root Guard.
* Desactive Cisco Discovery Protocol (CDP) en puertos que se enfrentan a redes desconocidas o que no son de confianza y que no requieren CDP para obtener resultados positivos. (CDP opera en la Capa 2 y podría proporcionar a los atacantes información que usted preferiría no revelar).
* En un conmutador nuevo, apague todos los puertos y asignarlos a una VLAN que no se use para nada más que un estacionamiento. Luego abra los puertos y asigne las VLAN correctas a medida que los puertos están asignados y sean necesarios.
* Utilice Root Guard para controlar qué puertos no pueden convertirse en puertos raíz para conmutadores remotos.
* Utilice DAI.
* Utilice IP Source Guard para evitar la suplantación de información de capa 3 por parte de los hosts.
* Implemente 802.1X cuando sea posible para autenticar y autorizar a los usuarios antes de permitirles comunicarse con el resto de la red.
* Utilice el espionaje del Protocolo de configuración dinámica de host (DHCP) para evitar que servidores DHCP no autorizados afecten a la red.
* Utilice el control de tormentas para limitar la cantidad de tráfico de transmisión o multidifusión que fluye a través de un conmutador. Un atacante podría realizar un ataque de tormenta de paquetes (o tormenta de difusión) para provocar una condición DoS. El atacante hace esto enviando transmisiones excesivas de paquetes IP (a menudo tráfico de difusión) en una red.
* Implemente listas de control de acceso (ACL), como ACL de capa 3 y capa 2, para controlar el tráfico y aplicar políticas.

### **Ataques de degradación**

En un ataque de degradación, un atacante obliga a un sistema a favorecer un protocolo de cifrado débil o un algoritmo hash que puede ser susceptible a otras vulnerabilidades. Un ejemplo de vulnerabilidad y ataque de degradación es la vulnerabilidad Padding Oracle on Downgraded Legacy Encryption (POODLE) en OpenSSL, que permitió al atacante negociar el uso de una versión inferior de TLS entre el cliente y el servidor.&#x20;

POODLE era una vulnerabilidad específica de OpenSSL y ha sido parcheada desde 2014. Sin embargo, en la práctica, eliminar la compatibilidad con versiones anteriores suele ser la única forma de evitar otros ataques o fallas de degradación.

**Lanzar Ettercap y Explorar sus Capacidades**

**1: Configurar un Ataque de ARP Spoofing**

1.  Usar SSH para iniciar sesión en el host de destino  con el usuario  y la contraseña .

    ```bash
    ssh -l username 10.6.6.23
    ```
2.  Verificar las entradas actuales en la caché ARP del host de destino usando el comando:

    ```bash
    ip neighbor
    ```

    (o usar `arp -a` si se está utilizando una versión de VM con CPU ARM, como Apple M1/M2).

**2: Cargar la interfaz gráfica de usuario de Ettercap para comenzar el escaneo**

1.  Usar el comando `ettercap -h` para ver el archivo de ayuda de Ettercap.

    ```bash
    ettercap -h
    ```
2.  Iniciar la interfaz gráfica de usuario de Ettercap usando el comando:

    ```bash
    sudo ettercap -G
    ```
3. Cambiar la interfaz de escucha a "br-internal" en la ventana de configuración.
4. Hacer clic en el ícono de la marca de verificación en la esquina superior derecha para iniciar el espionaje unificado.

**Realizar el Ataque en el Camino (MITM)**

**1: Seleccionar los Dispositivos Objetivo**

1. En la ventana GUI de Ettercap, abrir la lista de hosts.
2. Escanear los hosts en la red 10.6.6.0/24. **Respuesta:** Número de hosts descubiertos.
3. Seleccionar el host de usuario (10.6.6.23) y agregarlo como "Target 1".
4. Seleccionar el servidor web de destino (10.6.6.13) y agregarlo como "Target 2".
5. Hacer clic en el ícono de MITM y seleccionar "ARP Poisoning...". Verificar que "Sniff remote connections" esté seleccionado y hacer clic en OK.

**2: Realizar el Ataque de ARP Spoofing**

1. Volver a la ventana de la terminal SSH con el host de destino.
2. Repetir el ping a 10.6.6.13 y usar `ip neighbor` para ver la tabla ARP.&#x20;
3. Cerrar la interfaz gráfica de usuario de Ettercap sin cerrar la conexión SSH.

**Usar Wireshark para Observar el Ataque de ARP Spoofing**

**1: Seleccionar los Dispositivos Objetivo y Realizar el Ataque MITM usando la CLI**

1. En la terminal SSH conectada a 10.6.6.23, ejecutar pings a 10.6.6.11 y 10.6.6.13.
2. Usar `ip neighbor` para ver las direcciones MAC asociadas con las direcciones IP de los sistemas.

```
ping -c 5 10.6.6.11
ip neighbor
```

1. Usar el comando `sudo ettercap -T` para realizar el ataque en modo texto y guardar un archivo .pcap.
2.  Ejecutar el comando ettercap en la terminal:

    ```bash
    sudo ettercap -T -q -i br-internal --write mitm-saved.pcap --mitm arp /10.6.6.23// /10.6.6.13//
    ```

**2: Abrir Wireshark para ver el archivo PCAP guardado**

1. Examinar el archivo .pcap con Wireshark. **Respuesta:**
2.  En la ventana de la terminal Kali, iniciar Wireshark con el archivo mitm-saved.pcap:

    ```bash
    wireshark mitm-saved.pcap
    ```
