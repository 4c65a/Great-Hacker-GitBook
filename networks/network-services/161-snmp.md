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

# 161:SNMP

## ¿Que es SNMP?

El Protocolo simple de administración de red (SNMP) es un protocolo que se  utilizan para administrar dispositivos de red. En las implementaciones SNMP, cada dispositivo de red contiene un agente SNMP que se conecta con un servidor SNMP independiente . Un administrador puede utilizar SNMP para obtener información sobre el estado y la configuración de un dispositivo de red, cambiar la configuración y realizar otras tareas administrativas. Como puede imaginar, esto resulta muy atractivo para los atacantes porque pueden aprovechar las vulnerabilidades de SNMP para realizar acciones similares de forma maliciosa.

Existen varias versiones de SNMP. Las dos versiones más populares hoy en día son SNMPv2c y SNMPv3. SNMPv2c.

La información del dispositivo administrado se guarda en una base de datos llamada Base de información de administración (MIB).

**El puerto por default:**

```
PORT    STATE SERVICE REASON 
161/udp open  snmp    udp-response ttl 244   
```

## Escanear

```bash
nmap  –Pn –sU –p 161 192.168.56.110
```

```bash
nmap -p 161  -sU 192.123.11.21
```

### Script

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

<mark style="color:red;">**Recursos**</mark>

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/pentesting-snmp" %}
