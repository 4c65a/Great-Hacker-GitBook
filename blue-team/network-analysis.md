---
icon: server
---

# Network Analysis

## Captura en Vivo con TCPDump y TShark

### Interfaces disponibles

Antes de capturar, siempre verificá en qué interfaz querés escuchar.

**TCPDump:**

```bash
tcpdump -D
```

**TShark:**

```bash
tshark -D
```

***

### Capturar tráfico en vivo

**TCPDump:**

```bash
sudo tcpdump -i eth0
```

`-i` = interfaz (podés usar `any` para todas)

**TShark:**

```bash
sudo tshark -i eth0
```

***

### Guardar captura a un archivo `.pcap`

**TCPDump:**

```bash
sudo tcpdump -i eth0 -w captura.pcap
```

**TShark:**

```bash
sudo tshark -i eth0 -w captura.pcap
```

***

### Captura filtrada (por protocolo, puerto, IP, etc.)

**Solo tráfico HTTP (puerto 80):**

```bash
tcpdump -i eth0 port 80
tshark -i eth0 -f "port 80"
```

**Solo paquetes TCP:**

```bash
tcpdump -i eth0 tcp
tshark -i eth0 -f "tcp"
```

**Solo una IP:**

```bash
tcpdump -i eth0 host 192.168.1.5
tshark -i eth0 -f "host 192.168.1.5"
```

**IP origen y destino específicos:**

```bash
tcpdump -i eth0 src 192.168.1.2 and dst 10.0.0.5
```

***

### Número limitado de paquetes

```bash
tcpdump -i eth0 -c 100
tshark -i eth0 -c 100
```

***

### Capturar solo cabeceras (sin payload)

```bash
tcpdump -i eth0 -s 96
```

`-s` = snaplen. Para ver todo el paquete, usá `-s 0`.

***

### Visualización en consola (análisis en vivo)

**Mostrar contenido en ASCII:**

```bash
tcpdump -i eth0 -A
```

**Mostrar hex + ASCII:**

```bash
tcpdump -i eth0 -X
```

**Verbosidad y timestamp detallado:**

```bash
tcpdump -i eth0 -nnvvtttt
```

***

### Captura en background (modo análisis continuo)

**TCPDump:**

```bash
sudo nohup tcpdump -i eth0 -w /tmp/captura.pcap &
```

`nohup` evita que se corte si cerrás la terminal, `&` lo manda al background.

***

## Análisis de Capturas

### Leer archivos `.pcap`

**TCPDump:**

```bash
tcpdump -r archivo.pcap
```

**TShark:**

```bash
tshark -r archivo.pcap
```

***

### Filtros básicos en TCPDump

```bash
tcpdump -r archivo.pcap tcp
tcpdump -r archivo.pcap udp
tcpdump -r archivo.pcap port 80
tcpdump -r archivo.pcap 'tcp[tcpflags] == tcp-syn'
tcpdump -r archivo.pcap 'tcp[tcpflags] == 24'
tcpdump -r archivo.pcap 'icmp[0] == 8'
```

***

### Opciones útiles de visualización

```bash
tcpdump -r archivo.pcap -nnvvX
```

***

### Extracción de datos con comandos de texto

**cut**

```bash
tcpdump -r archivo.pcap | cut -d ">" -f 1
```

**awk**

```bash
tcpdump -r archivo.pcap | awk '{print $7}'
awk '{print $(NF-2)}'
```

**grep**

```bash
tcpdump -r archivo.pcap -A | grep "zip"
```

***

### TShark: potencia de Wireshark en consola

**Filtrar por protocolo:**

```bash
tshark -r archivo.pcap -Y http
```

**Mostrar solo IPs:**

```bash
tshark -r archivo.pcap -T fields -e ip.src -e ip.dst
```

**Ver flags TCP:**

```bash
tshark -r archivo.pcap -Y "tcp.flags.syn == 1 && tcp.flags.ack == 1"
```

**Ver contenido de aplicación:**

```bash
tshark -r archivo.pcap -Y "http.request" -T fields -e http.host -e http.request.uri
```

***

### Crear resumen estadístico

**Con TShark:**

```bash
tshark -r archivo.pcap -q -z io,phs
```

**Con TCPDump + sort + uniq:**

```bash
tcpdump -r archivo.pcap | awk '{print $3}' | cut -d "." -f1-4 | sort | uniq -c | sort -nr
```

***

### Ejemplo: análisis de tráfico sospechoso

```bash
tcpdump -r captura.pcap 'tcp[tcpflags] == 24' -nn -tttt -A | grep -i "user\|pass"
```

***

### Resumen de flags TCP (valores binarios)

Ej: `tcp[tcpflags] == 24` (PSH 8 + ACK 16)

***

## Inteligencia con TCPDump, TShark y Bash

### Detectar Port Scanning (SYN scan / Nmap)

```bash
tcpdump -n -r captura.pcap 'tcp[tcpflags] == 2' | awk '{print $3}' | cut -d'.' -f1-4 | sort | uniq -c | sort -nr | head
```

***

### Detectar conexiones completas (3-way handshake)

```bash
tshark -r captura.pcap -Y "tcp.flags.syn == 1 and tcp.flags.ack == 0" -T fields -e ip.src -e tcp.srcport
tshark -r captura.pcap -Y "tcp.flags.syn == 1 and tcp.flags.ack == 1" -T fields -e ip.dst -e tcp.dstport
```

***

### Extraer archivos o strings sospechosos

```bash
tcpdump -A -r captura.pcap | grep -i -E "\.zip|\.exe|\.rar"
tcpdump -A -r captura.pcap | grep -i -E "pass|login|usuario|clave"
```

***

### Estadísticas de tráfico con TShark

```bash
tshark -r captura.pcap -q -z io,stat,0,ip,tcp,udp,icmp
tshark -r captura.pcap -q -z conv,ip
```

***

### Análisis pasivo de contraseñas HTTP

```bash
tshark -r captura.pcap -Y "http.request.method == POST" -T fields -e ip.src -e http.host -e http.file_data
```

***

### Captura de tráfico con rotación&#x20;

```bash
sudo tcpdump -i eth0 -C 10 -W 5 -w captura.pcap
```

***

### Convertir `.pcap` en JSON o CSV

**CSV:**

```bash
tshark -r captura.pcap -T fields -e frame.time -e ip.src -e ip.dst -e tcp.srcport -e tcp.dstport -E separator=, > salida.csv
```

**JSON:**

```bash
tshark -r captura.pcap -T json > salida.json
```

***

### Live Sniffing + Análisis en tiempo real

```bash
tcpdump -i eth0 -l -A | grep -iE "user|pass|cookie"
```

`-l` permite que el output se vea en vivo.

