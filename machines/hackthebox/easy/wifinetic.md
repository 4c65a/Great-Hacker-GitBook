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

# Wifinetic

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## Escaneo de la máquina.

```bash
nmap -sV -sC 10.10.11.247  -oA initial 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-09-14 23:23 EDT
Nmap scan report for 10.10.11.247
Host is up (0.20s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE    SERVICE    VERSION
21/tcp    open     ftp        vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.14.93
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-r--r--    1 ftp      ftp          4434 Jul 31 11:03 MigrateOpenWrt.txt
| -rw-r--r--    1 ftp      ftp       2501210 Jul 31 11:03 ProjectGreatMigration.pdf
| -rw-r--r--    1 ftp      ftp         60857 Jul 31 11:03 ProjectOpenWRT.pdf
| -rw-r--r--    1 ftp      ftp         40960 Sep 11 15:25 backup-OpenWrt-2023-07-26.tar
|_-rw-r--r--    1 ftp      ftp         52946 Jul 31 11:03 employees_wellness.pdf
22/tcp    open     ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 48add5b83a9fbcbef7e8201ef6bfdeae (RSA)
|   256 b7896c0b20ed49b2c1867c2992741c1f (ECDSA)
|_  256 18cd9d08a621a8b8b6f79f8d405154fb (ED25519)
53/tcp    open     tcpwrapped
15003/tcp filtered unknown
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 49.08 seconds


```

### Realizar prueba con FTP

```bash
ftp 10.10.11.247
```

```bash
ftp> ls
229 Entering Extended Passive Mode (|||41883|)
150 Here comes the directory listing.
-rw-r--r--    1 ftp      ftp          4434 Jul 31 11:03 MigrateOpenWrt.txt
-rw-r--r--    1 ftp      ftp       2501210 Jul 31 11:03 ProjectGreatMigration.pdf
-rw-r--r--    1 ftp      ftp         60857 Jul 31 11:03 ProjectOpenWRT.pdf
-rw-r--r--    1 ftp      ftp         40960 Sep 11 15:25 backup-OpenWrt-2023-07-26.tar                                                                         
-rw-r--r--    1 ftp      ftp         52946 Jul 31 11:03 employees_wellness.pdf
226 Directory send OK.

```

```bash
ftp> prompt off
Interactive mode off.
ftp> mget *
local: MigrateOpenWrt.txt remote: MigrateOpenWrt.txt
229 Entering Extended Passive Mode (|||46603|)
150 Opening BINARY mode data connection for MigrateOpenWrt.txt (4434 bytes).
100% |****************************************************|  4434       12.66 MiB/s    00:00 ETA226 Transfer complete.
4434 bytes received in 00:00 (45.51 KiB/s)
local: ProjectGreatMigration.pdf remote: ProjectGreatMigration.pdf
229 Entering Extended Passive Mode (|||43303|)
150 Opening BINARY mode data connection for ProjectGreatMigration.pdf (2501210 bytes).
100% |****************************************************|  2442 KiB    1.19 MiB/s    00:00 ETA226 Transfer complete.
2501210 bytes received in 00:02 (1.14 MiB/s)
local: ProjectOpenWRT.pdf remote: ProjectOpenWRT.pdf
229 Entering Extended Passive Mode (|||41309|)
150 Opening BINARY mode data connection for ProjectOpenWRT.pdf (60857 bytes).
100% |****************************************************| 60857      312.13 KiB/s    00:00 ETA226 Transfer complete.
60857 bytes received in 00:00 (208.67 KiB/s)
local: backup-OpenWrt-2023-07-26.tar remote: backup-OpenWrt-2023-07-26.tar
229 Entering Extended Passive Mode (|||48627|)
150 Opening BINARY mode data connection for backup-OpenWrt-2023-07-26.tar (40960 bytes).
100% |****************************************************| 40960      418.15 KiB/s    00:00 ETA226 Transfer complete.
40960 bytes received in 00:00 (210.50 KiB/s)
local: employees_wellness.pdf remote: employees_wellness.pdf
229 Entering Extended Passive Mode (|||45844|)
150 Opening BINARY mode data connection for employees_wellness.pdf (52946 bytes).
100% |****************************************************| 52946      271.76 KiB/s    00:00 ETA226 Transfer complete.
52946 bytes received in 00:00 (181.35 KiB/s)
```
