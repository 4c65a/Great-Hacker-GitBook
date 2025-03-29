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

# Omisión del control de acceso a la red (NAC)

NAC es una tecnología diseñada para interrogar puntos finales antes de unirse a una red cableada o inalámbrica. Normalmente se utiliza junto con 802.1X para la gestión y el cumplimiento de identidades.&#x20;

Se puede configurar un conmutador de acceso a la red o un punto de acceso inalámbrico (AP) para autenticar a los usuarios finales y realizar una evaluación de la postura de seguridad del dispositivo terminal para hacer cumplir la política. Por ejemplo, puede comprobar si tiene software de seguridad como antivirus, antimalware y cortafuegos personales antes de permitirle unirse a la red. También puede verificar si tiene una versión específica de un sistema operativo y si su sistema ha sido parcheado para vulnerabilidades específicas.

Además, los dispositivos habilitados para NAC pueden utilizar varias técnicas de detección para detectar el punto final que intenta conectarse a la red. Un dispositivo habilitado para NAC intercepta solicitudes DHCP desde puntos finales. Un oyente de difusión se utiliza para buscar tráfico de red, como solicitudes ARP y solicitudes DHCP generadas por puntos finales.

Varias soluciones NAC utilizan agentes basados ​​en el cliente para realizar evaluaciones de la postura de seguridad de los terminales para evitar que un terminal se una a la red hasta que sea evaluado. Además, algunos conmutadores se pueden configurar para enviar un mensaje de captura SNMP cuando se registra una nueva dirección MAC en un determinado puerto del conmutador y para activar el proceso NAC.

Las implementaciones de NAC pueden permitir que nodos específicos, como impresoras, teléfonos IP y equipos de videoconferencia, se unan a la red mediante el uso de una lista permitida o whitelist de direcciones MAC correspondientes a dichos dispositivos. Este proceso se conoce como _omisión de autenticación MAC (auth)_ . La omisión de autenticación MAC es una característica de NAC. El administrador de la red puede preconfigurar o cambiar manualmente estos niveles de acceso.

Un administrador debe predefinir manualmente un dispositivo que accede a una VLAN específica  para un puerto específico, lo que hace que la implementación de una política de red dinámica en múltiples puertos utilizando la seguridad de puerto sea extremadamente difícil de mantener.

Un atacante podría falsificar fácilmente una dirección MAC autorizada  y omitir una configuración de NAC. Por ejemplo, es posible falsificar la dirección MAC de un teléfono IP y utilizarla para conectarse a una red. Esto se debe a que un puerto para el cual está habilitada la omisión de autenticación MAC se puede habilitar o deshabilitar dinámicamente según la dirección MAC del dispositivo que se conecta a él.

