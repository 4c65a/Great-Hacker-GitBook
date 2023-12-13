# SMB enumeracion

SNMP se basa en UDP, un protocolo simple y sin estado, por lo que es susceptible a ataques de suplantación de IP y de repetición. Además, los protocolos SNMP comúnmente utilizados 1, 2 y 2c no ofrecen encriptación de tráfico, lo que significa que la información y credenciales de SNMP pueden ser fácilmente interceptadas en una red local. Los protocolos SNMP tradicionales también cuentan con esquemas de autenticación débiles y a menudo se dejan configurados con las cadenas de comunidad predeterminadas públicas y privadas.

La Base de Información de Administración de SNMP (MIB, por sus siglas en inglés) es una base de datos que contiene información generalmente relacionada con la administración de redes. La base de datos está organizada como un árbol, con ramas que representan diferentes organizaciones o funciones de red.&#x20;

Para escanear puertos SNMP abiertos, podemos utilizar nmap, utilizando la opción -sU para realizar un escaneo UDP y la opción --open para limitar la salida y mostrar solo los puertos abiertos.

```bash
sudo nmap -sU --open -p 161 192.168.50.1-254 -oG open-snmp.txt
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-14 06:02 EDT
Nmap scan report for 192.168.50.151
Host is up (0.10s latency).
PORT     STATE SERVICE
161/udp  open  snmp
Nmap done: 1 IP address (1 host up) scanned in 0.49 seconds
```

Alternativamente, podemos utilizar una herramienta como onesixtyone, que intentará un ataque de fuerza bruta contra una lista de direcciones IP. Primero, debemos construir archivos de texto que contengan cadenas de comunidad y las direcciones IP que deseamos escanear.

```bash
echo public > community
echo private >> community
echo manager >> community
for ip in $(seq 1 254); do echo 192.168.50.$ip; done > ips
onesixtyone -c community -i ips

Scanning 254 hosts, 3 communities
192.168.50.151 [public] Hardware: Intel64 Family 6 Model 79 Stepping 1 AT/AT
COMPATIBLE - Software: Windows Version 6.3 (Build 17763 Multiprocessor Free)
```

Podemos sondear y consultar valores SNMP utilizando una herramienta como snmpwalk, siempre y cuando conozcamos la cadena de comunidad de solo lectura de SNMP, que en la mayoría de los casos es "public".

Utilizando algunos de los valores MIB.Este comando enumera todo el árbol MIB usando la opción -c para especificar la cadena de comunidad y -v para especifica el número de versión SNMP, así como la opción -t 10 para aumentar el período de tiempo de espera a 10 segundos:

```bash
snmpwalk -c public -v1 -t 10 192.168.50.151
iso.3.6.1.2.1.1.1.0 = STRING: "Hardware: Intel64 Family 6 Model 79 Stepping 1 AT/AT COMPATIBLE - Software: Windows Version 6.3 (Build 17763 Multiprocessor Free)"
iso.3.6.1.2.1.1.2.0 = OID: iso.3.6.1.4.1.311.1.1.3.1.3
iso.3.6.1.2.1.1.3.0 = Timeticks: (78235) 0:13:02.35
iso.3.6.1.2.1.1.4.0 = STRING: "admin@megacorptwo.com"
iso.3.6.1.2.1.1.5.0 = STRING: "dc01.megacorptwo.com"
iso.3.6.1.2.1.1.6.0 = ""
iso.3.6.1.2.1.1.7.0 = INTEGER: 79
iso.3.6.1.2.1.2.1.0 = INTEGER: 24
...
```

Usaremos el comando snmpwalk, que puede analizar una rama específica del Árbol MIB llamada OID.276

El siguiente ejemplo enumera los usuarios de Windows en la máquina dc01:

```bash
snmpwalk -c public -v1 192.168.50.151 1.3.6.1.4.1.77.1.2.25
iso.3.6.1.4.1.77.1.2.25.1.1.5.71.117.101.115.116 = STRING: "Guest"
iso.3.6.1.4.1.77.1.2.25.1.1.6.107.114.98.116.103.116 = STRING: "krbtgt"
iso.3.6.1.4.1.77.1.2.25.1.1.7.115.116.117.100.101.110.116 = STRING: "student"
iso.3.6.1.4.1.77.1.2.25.1.1.13.65.100.109.105.110.105.115.116.114.97.116.111.114 = STRING: "Administrator"
```

Nuestra orden consultó una sub-rama específica de MIB que está mapeada a todos los nombres de cuenta de usuario locales.

Como otro ejemplo, podemos enumerar todos los procesos que se están ejecutando actualmente:

```bash
snmpwalk -c public -v1 192.168.50.151 1.3.6.1.2.1.25.4.2.1.2
iso.3.6.1.2.1.25.4.2.1.2.1 = STRING: "System Idle Process"
iso.3.6.1.2.1.25.4.2.1.2.4 = STRING: "System"
iso.3.6.1.2.1.25.4.2.1.2.88 = STRING: "Registry"
iso.3.6.1.2.1.25.4.2.1.2.260 = STRING: "smss.exe"
iso.3.6.1.2.1.25.4.2.1.2.316 = STRING: "svchost.exe"
iso.3.6.1.2.1.25.4.2.1.2.372 = STRING: "csrss.exe"
iso.3.6.1.2.1.25.4.2.1.2.472 = STRING: "svchost.exe"
iso.3.6.1.2.1.25.4.2.1.2.476 = STRING: "wininit.exe"
iso.3.6.1.2.1.25.4.2.1.2.484 = STRING: "csrss.exe"
iso.3.6.1.2.1.25.4.2.1.2.540 = STRING: "winlogon.exe"
iso.3.6.1.2.1.25.4.2.1.2.616 = STRING: "services.exe"
iso.3.6.1.2.1.25.4.2.1.2.632 = STRING: "lsass.exe"
iso.3.6.1.2.1.25.4.2.1.2.680 = STRING: "svchost.exe"
```

El comando devolvió una serie de cadenas, cada una de ellas contiene el nombre del proceso en ejecución. Esta información podría ser valiosa ya que podría revelar aplicaciones vulnerables o incluso indicar qué tipo de antivirus se está ejecutando en el objetivo.

De manera similar, podemos consultar todo el software instalado en la máquina:

```bash
snmpwalk -c public -v1 192.168.50.151 1.3.6.1.2.1.25.6.3.1.2
iso.3.6.1.2.1.25.6.3.1.2.1 = STRING: "Microsoft Visual C++ 2019 X64 Minimum Runtime - 14.27.29016"
iso.3.6.1.2.1.25.6.3.1.2.2 = STRING: "VMware Tools"
iso.3.6.1.2.1.25.6.3.1.2.3 = STRING: "Microsoft Visual C++ 2019 X64 Additional Runtime - 14.27.29016"
iso.3.6.1.2.1.25.6.3.1.2.4 = STRING: "Microsoft Visual C++ 2015-2019 Redistributable (x86) - 14.27.290"
iso.3.6.1.2.1.25.6.3.1.2.5 = STRING: "Microsoft Visual C++ 2015-2019 Redistributable (x64) - 14.27.290"
iso.3.6.1.2.1.25.6.3.1.2.6 = STRING: "Microsoft Visual C++ 2019 X86 Additional Runtime - 14.27.29016"
iso.3.6.1.2.1.25.6.3.1.2.7 = STRING: "Microsoft Visual C++ 2019 X86 Minimum Runtime - 14.27.29016"
...
```

Cuando se combina con la lista de procesos en ejecución que obtuvimos anteriormente, esta información puede ser extremadamente valiosa para verificar la versión exacta del software que se está ejecutando en el host objetivo.

Otra técnica de enumeración SNMP es listar todos los puertos TCP en escucha actualmente:

```bash
snmpwalk -c public -v1 192.168.50.151 1.3.6.1.2.1.6.13.1.3
iso.3.6.1.2.1.6.13.1.3.0.0.0.0.88.0.0.0.0.0 = INTEGER: 88
iso.3.6.1.2.1.6.13.1.3.0.0.0.0.135.0.0.0.0.0 = INTEGER: 135
iso.3.6.1.2.1.6.13.1.3.0.0.0.0.389.0.0.0.0.0 = INTEGER: 389
iso.3.6.1.2.1.6.13.1.3.0.0.0.0.445.0.0.0.0.0 = INTEGER: 445
iso.3.6.1.2.1.6.13.1.3.0.0.0.0.464.0.0.0.0.0 = INTEGER: 464
iso.3.6.1.2.1.6.13.1.3.0.0.0.0.593.0.0.0.0.0 = INTEGER: 593
iso.3.6.1.2.1.6.13.1.3.0.0.0.0.636.0.0.0.0.0 = INTEGER: 636
iso.3.6.1.2.1.6.13.1.3.0.0.0.0.3268.0.0.0.0.0 = INTEGER: 3268
iso.3.6.1.2.1.6.13.1.3.0.0.0.0.3269.0.0.0.0.0 = INTEGER: 3269
iso.3.6.1.2.1.6.13.1.3.0.0.0.0.5357.0.0.0.0.0 = INTEGER: 5357
iso.3.6.1.2.1.6.13.1.3.0.0.0.0.5985.0.0.0.0.0 = INTEGER: 5985
```

