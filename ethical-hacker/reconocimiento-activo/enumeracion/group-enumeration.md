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

# Group Enumeration

Para un probador de penetración, la enumeración de grupos es útil para determinar los roles de autorización que se utilizan en el entorno de destino. El script Nmap NSE para enumerar grupos SMB es smb-enum-groups. Este script intenta extraer una lista de grupos de una máquina remota con Windows. También puede revelar la lista de usuarios que son miembros de esos grupos. La sintaxis del comando es la siguiente:

```
nmap --script smb-enum-groups.nse -p445 192.168.1.251
```
