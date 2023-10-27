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

# Script

## DNS nmap script

```bash
nmap --script=broadcast-dns-service-discovery google.com
```

```bash
nmap -Pn -sU --script=dns-check-zone -p 53 google.com
```

```bash
nmap -sU -p 53 --script=dns-recursion
```

```bash
nmap -sS --script=dns-*
```

### DNS nmap script brute&#x20;

```bash
nmap -T4 -p 53 --script dns-brute
```
