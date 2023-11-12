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

# Ataques de inanición de DHCP y servidores DHCP no autorizados

Los ataques más comunes contra servidores DHCP en las organizaciones son la inanición de DHCP y la suplantación de DHCP con servidores no autorizados. En el ataque de inanición de DHCP, un agresor envía una gran cantidad de mensajes DHCP REQUEST con direcciones MAC falsificadas. Si el servidor DHCP responde a todos estos mensajes falsos, las direcciones IP disponibles se agotan rápidamente. Después de agotar las direcciones IP, el atacante puede configurar un servidor DHCP no autorizado y responder a nuevas solicitudes DHCP de los clientes en la red.

En el ataque de suplantación de DHCP, el atacante configura un servidor DHCP fraudulento para responder a las solicitudes de los clientes DHCP. Puede configurar la dirección IP de la puerta de enlace predeterminada y el servidor DNS para interceptar el tráfico de los hosts de la red. Esto permite al atacante realizar ataques man-in-the-middle y recopilar información del tráfico de la red.

Se muestra un ejemplo de una herramienta llamada Yersenia que se puede utilizar para configurar un servidor DHCP no autorizado y lanzar ataques de suplantación y falta de DHCP. Esta herramienta proporciona a los atacantes la capacidad de ejecutar estos ataques de manera efectiva y comprometer la integridad de la red.
