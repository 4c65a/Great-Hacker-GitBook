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

# DNS Lookups

### Para ver mas comandos y herramientas ir a [53-dns.md](../../pentesting-networks/53-dns.md "mention")

### Enumeración&#x20;

```bash
dnsrecon -d google.com
```

```bash
nmap --script=broadcast-dns-service-discovery
```

```bash
nmap -sU -p 53 --script=dns-recursion
```

```bash
fierce --domain google.com
```

Enumeración todo en uno

```bash
nmap -sS --script=dns-*
```

### Recuperación de registros DNS

```bash
dnsrecon -d google.com -t std
```

### Reverse Lookup

```bash
dnsrecon -r 173.158.10.1/16
```

```bash
dig -x 173.158.10.1/16
```

```bash
host -l 192.168.1.1
```

```bash
nslookup -type=ptr 192.168.1.1
```

```bash
dig -x 2a00:1450:400c:c06::93 @<DNS_IP>
```

### DNS nmap script

```bash
nmap --script=broadcast-dns-service-discovery google.com
```

