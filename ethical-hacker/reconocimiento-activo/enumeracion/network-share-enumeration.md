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

# Network Share Enumeration

Identificar los sistemas de una red que están compartiendo archivos, carpetas e impresoras es útil para crear una superficie de ataque de una red interna. El script Nmap smb-enum-shares utiliza la llamada a procedimiento remoto de Microsoft (MSRPC) para la enumeración de recursos compartidos en red. La sintaxis del script Nmap smb-enum-shares.nse es la siguiente:

```
nmap --script smb-enum-shares.nse -p 445 192.168.1.251
```
