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

# Broker

`10.10.11.243 Ip`

## Realizar un escaner de puertos con nmap.

```
sudo nmap -sS -p- -Pn --open 10.10.11.243 -vvv
```

**Puertos descubiertos**&#x20;

```
───────┼───────────────────────────────────────────────────────────────────────────────────────
   1   │ PORT      STATE SERVICE     REASON
   2   │ 22/tcp    open  ssh         syn-ack ttl 63
   3   │ 80/tcp    open  http        syn-ack ttl 63
   4   │ 1883/tcp  open  mqtt        syn-ack ttl 63
   5   │ 5672/tcp  open  amqp        syn-ack ttl 63
   6   │ 8161/tcp  open  patrol-snmp syn-ack ttl 63
   7   │ 40157/tcp open  unknown     syn-ack ttl 63
   8   │ 61613/tcp open  unknown     syn-ack ttl 63
   9   │ 61614/tcp open  unknown     syn-ack ttl 63
  10   │ 61616/tcp open  unknown     syn-ack ttl 63
```

