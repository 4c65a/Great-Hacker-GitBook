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

# Utilidades de comando y control (C2)

Los atacantes suelen utilizar sistemas de comando y control (denominados C2 o CnC) para enviar comandos e instrucciones a los sistemas comprometidos. El C2 puede ser el sistema del atacante (una computadora de escritorio, una computadora portátil) o un servidor físico o virtual dedicado. Un C2 crea un canal encubierto con el sistema comprometido. Un canal encubierto es una técnica adversarial que permite al atacante transferir objetos de información entre procesos o sistemas que, según una política de seguridad, no deberían poder comunicarse.

Los atacantes suelen utilizar máquinas virtuales en un servicio en la nube o incluso utilizar otros sistemas comprometidos como servidores C2. Incluso se han utilizado servicios como Twitter, Dropbox y Photobucket para tareas C2. La comunicación C2 puede ser tan simple como mantener una baliza temporizada, o "latido", para lanzar ataques adicionales o para la filtración de datos.&#x20;

Se pueden utilizar muchas técnicas y utilidades diferentes para crear un C2. Seleccione cada uno de los siguientes ejemplos para obtener más información.

**socat**\
Una utilidad C2 que se puede utilizar para crear múltiples shells inversos (consulte [_http://www.dest-unreach.org/socat_](http://www.dest-unreach.org/socat) )

**wsc2**\
Una utilidad C2 basada en Python que utiliza WebSockets (consulte [_https://github.com/Arno0x/WSC2_](https://github.com/Arno0x/WSC2) )

**Implante WMI**\
Una herramienta basada en PowerShell que aprovecha WMI para crear un canal C2 (consulte [_https://github.com/ChrisTruncer/WMImplant_](https://github.com/ChrisTruncer/WMImplant) )

**DropboxC2 (DBC2)**\
Una utilidad C2 que usa Dropbox (consulte [_https://github.com/Arno0x/DBC2_](https://github.com/Arno0x/DBC2) )

**trevorc2**\
Una utilidad C2 basada en Python creada por Dave Kennedy de TrustedSec (consulte [_https://github.com/trustedsec/trevorc2_](https://github.com/trustedsec/trevorc2) )

**Gorjeo**\
Una utilidad C2 que utiliza mensajes directos de Twitter para comando y control (ver [_https://github.com/PaulSec/twittor_](https://github.com/PaulSec/twittor) )

**DNSCat2**\
Una utilidad C2 basada en DNS que admite cifrado y que ha sido utilizada por malware, actores de amenazas y evaluadores de penetración (consulte [_https://github.com/iagox86/dnscat2_](https://github.com/iagox86/dnscat2) )
