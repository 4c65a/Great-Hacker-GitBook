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

# Salto de VLAN

En una red local (LAN), los dispositivos comparten una dirección de red IP de Capa 3 y están en el mismo dominio de transmisión de Capa 2. Una VLAN (Virtual LAN) es un dominio de difusión de Capa 2 controlado por un conmutador. Los dispositivos en una VLAN están asociados con un conmutador, y los puertos del conmutador determinan la pertenencia a una VLAN. En una configuración predeterminada, todos los puertos están asignados a la VLAN 1.

A medida que se agregan más usuarios, es posible dividirlos en subredes y VLAN diferentes. Los puertos del conmutador se asignan a VLAN, y los dispositivos conectados a esos puertos son miembros de esas VLAN. La configuración de DHCP se utiliza para asignar direcciones IP comunes a dispositivos en una VLAN.

Para permitir la comunicación entre dispositivos en VLAN separadas pero en diferentes conmutadores, se utilizan puertos troncales que etiquetan el tráfico con información de VLAN. Los ataques relacionados con VLAN incluyen el salto de VLAN, donde un atacante obtiene acceso al tráfico de otras VLAN. Los métodos incluyen la suplantación de conmutador y el etiquetado doble, donde se agregan dos etiquetas VLAN a una trama.

Se recomienda seguir mejores prácticas, cómo evitar el uso de la VLAN 1, apagar todos los puertos en un nuevo conmutador y asignar VLAN específicas según sea necesario para mitigar riesgos de seguridad, como saltos de VLAN. El ataque de etiquetado doble implica agregar dos etiquetas VLAN a una trama, y el conmutador solo procesa la etiqueta externa, lo que puede ser explotado por un atacante para acceder a otras VLAN.

\
