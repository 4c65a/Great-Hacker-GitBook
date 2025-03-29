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

# 68:DHCP

## ¿Que es DHCP?

Es que es el mecanismo estándar para asignar dinámicamente direcciones IP dentro de una red. Significa Protocolo de configuración dinámica de host.

El direccionamiento IP, o Protocolo de Internet, es un medio lógico para asignar direcciones a dispositivos en una red. Cada dispositivo conectado a una red requiere una dirección IP única.

## Escanear

`nmap -sU --script broadcast-dhcp-discover -p 67,68`

```
PORT     STATE SERVICE               VERSION
68/udp   open  dhcp  
```

### Script

```
nmap -sU --script broadcast-dhcp-discover -p 67,68 <target-ip>
```

