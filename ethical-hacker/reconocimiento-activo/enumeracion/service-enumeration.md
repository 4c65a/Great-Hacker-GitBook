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

# Service Enumeration

La enumeración de servicios es el proceso de identificar los servicios que se ejecutan en un sistema remoto, y es uno de los principales objetivos de Nmap como escáner de puertos. La discusión anterior en este módulo destaca los diversos tipos de escaneo y cómo pueden usarse para eludir filtros. Cuando está conectado a un sistema que se encuentra en un segmento de red conectado directamente, puede ejecutar algunos scripts adicionales para enumerar más a fondo. Un escaneo de puertos toma la perspectiva de un usuario remoto autorizado. El script Nmap smb-enum-processes NSE enumera los servicios en un sistema Windows, y lo hace utilizando las credenciales de un usuario que tiene acceso para leer el estado de los servicios que se están ejecutando. Esta es una herramienta útil para consultar de forma remota un sistema Windows para determinar la lista exacta de servicios que se están ejecutando. La sintaxis del comando es la siguiente:

```
nmap --script smb-enum-processes.nse --script-args smbusername=<username>, smbpass=<password> -p445 <host>
```
