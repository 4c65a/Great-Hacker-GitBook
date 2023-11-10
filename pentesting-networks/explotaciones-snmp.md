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

# Explotaciones SNMP

Un ataque SNMP común implica que un atacante enumere los servicios SNMP y luego verifique las contraseñas SNMP predeterminadas configuradas. Desafortunadamente, este es uno de los principales defectos de muchas implementaciones porque muchos usuarios dejan credenciales SNMP débiles o predeterminadas en los dispositivos de red. SNMPv3 utiliza nombres de usuario y contraseñas y es más seguro que todas las versiones SNMP anteriores. Sin embargo, los atacantes aún pueden realizar ataques de diccionario y de fuerza bruta contra implementaciones SNMPv3. Una implementación más moderna y segura implica el uso de NETCONF con dispositivos de infraestructura más nuevos (como enrutadores y conmutadores).

```
snmp-brute.nse
snmp-hh3c-logins.nse
snmp-info.nse
snmp-interfaces.nse
snmp-ios-config.nse
snmp-netstat.nse
snmp-processes.nse
snmp-sysdescr.nse
snmp-win32-services.nse
snmp-win32-shares.nse
snmp-win32-software.nse
snmp-win32-users.nse
```

Cambie siempre las contraseñas predeterminadas! Como práctica recomendada, también debe limitar el acceso SNMP solo a hosts confiables y bloquear el puerto UDP 161 para cualquier sistema que no sea de confianza. Otra mejor práctica es utilizar SNMPv3 en lugar de versiones anteriores.
