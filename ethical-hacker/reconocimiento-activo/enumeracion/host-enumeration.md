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

# Host Enumeration

Enumeración de hosts es el proceso de identificar los hosts activos en una red. Esto se puede hacer enviando paquetes de ping a todas las direcciones IP en una red y observando las respuestas. Los hosts activos responderán a los paquetes de ping, mientras que los hosts inactivos no lo harán.

## Se puede hacer con nmap [-sn](../nmap/#host-discovery-scan-sn)

```
Nmap -sn 192.168.1.10
```

### Gobuster host virtuales

`vhost` descubre nombres de host virtuales en los servidores web de destino.

```
gobuster vhost -u https://example.com -t 50 -w /wordlists/Discovery/DNS/subdomains-top1million-5000.txt
```
