---
description: >-
  SSRF using CRLF injection, Lateral movement, API, LFI, privilege escalation,
  docker.
---

# Cybermonday

```
IP = 10.10.11.228 
```

## HOST

```
10.10.11.228 cybermonday.htb
```

## Reconocimiento

<figure><img src="../../../.gitbook/assets/Inicio.png" alt=""><figcaption></figcaption></figure>

### NMAP

```
sudo nmap -sS -p- -Pn --open 10.10.11.228 -vvv -oG PORT.txt
[sudo] password for titan:
Starting Nmap 7.94 ( https://nmap.org ) at 2023-12-10 21:52 UTC
Initiating SYN Stealth Scan at 21:52
Scanning cybermonday.htb (10.10.11.228) [65535 ports]
Discovered open port 22/tcp on 10.10.11.228
Discovered open port 80/tcp on 10.10.11.228
SYN Stealth Scan Timing: About 41.98% done; ETC: 21:53 (0:00:43 remaining)
Completed SYN Stealth Scan at 21:54, 86.17s elapsed (65535 total ports)
Nmap scan report for cybermonday.htb (10.10.11.228)
Host is up, received user-set (0.41s latency).
Scanned at 2023-12-10 21:52:35 UTC for 87s
Not shown: 64514 closed tcp ports (reset), 1019 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack ttl 63
80/tcp open  http    syn-ack ttl 62

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 86.26 seconds
           Raw packets sent: 85490 (3.762MB) | Rcvd: 78122 (3.215MB)
```

**Servicios**

```
nmap -sV -p 80,22  10.10.11.228
Starting Nmap 7.94 ( https://nmap.org ) at 2023-12-10 22:05 UTC
Nmap scan report for cybermonday.htb (10.10.11.228)
Host is up (0.22s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
80/tcp open  http    nginx 1.25.1
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.99 seconds
```

**SSH**

```
nmap -p 22 --script ssh-brute  10.10.11.228
```

