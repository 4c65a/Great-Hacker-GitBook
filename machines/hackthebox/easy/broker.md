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

### Servicios de puertos

```
 sudo nmap -sV -p 22,80,1883,5672,8161,40157,61613,61614,61616  10.10.11.243 -vvv
```

```
PORT      STATE SERVICE    REASON         VERSION
22/tcp    open  ssh        syn-ack ttl 63 OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
80/tcp    open  http       syn-ack ttl 63 nginx 1.18.0 (Ubuntu)
1883/tcp  open  mqtt       syn-ack ttl 63
5672/tcp  open  amqp?      syn-ack ttl 63
8161/tcp  open  http       syn-ack ttl 63 Jetty 9.4.39.v20210325
40157/tcp open  tcpwrapped syn-ack ttl 63
61613/tcp open  stomp      syn-ack ttl 63 Apache ActiveMQ
61614/tcp open  http       syn-ack ttl 63 Jetty 9.4.39.v20210325
61616/tcp open  apachemq   syn-ack ttl 63 ActiveMQ OpenWire transport
```

## Ir al navegador&#x20;

**Cuando fui al navegador a la direccion `10.10.11.243 Ip.`**

<figure><img src="../../../.gitbook/assets/SignIn.png" alt=""><figcaption></figcaption></figure>

**Realice una pruba con contraseña y usuario basica: admin y admin y logre ingresar a este sitio.**

<figure><img src="../../../.gitbook/assets/ActiveMQ.png" alt=""><figcaption></figcaption></figure>

**Hasta ahora puedo saber que utiliza el servicio ActiveMQ ,tambien lo descubrimos con nmap.**

```
   1  | 61613/tcp open  stomp      syn-ack ttl 63 Apache ActiveMQ
   2  │ 61616/tcp open  apachemq   syn-ack ttl 63 ActiveMQ OpenWire transport
```
