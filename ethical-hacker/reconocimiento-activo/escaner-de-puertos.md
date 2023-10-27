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

# Escáner de Puertos

## Escanear puerto con nmap

Un escaneo de puertos es un escaneo activo en el que la herramienta de escaneo envía varios tipos de sondas a la dirección IP de destino y luego examina las respuestas para determinar si el servicio está realmente escuchando. Por ejemplo, con un escaneo SYN de Nmap, la herramienta envía un paquete SYN TCP al puerto TCP que está sondeando. Este proceso también se conoce como escaneo semiabierto porque no abre una conexión TCP completa.

Si la respuesta es un SYN/ACK, esto indicaría que el puerto está realmente en un estado de escucha. Si la respuesta al paquete SYN es un RST (reset), esto indicaría que el puerto está cerrado o no está en un estado de escucha. Si la sonda SYN no recibe respuesta, Nmap lo marca como filtrado porque no puede determinar si el puerto está abierto o cerrado.

### Comandos

#### Scan SYN -sS

El parámetro `-sS` indica a Nmap que utilice un escaneo SYN. Este tipo de escaneo es el más común y se utiliza para identificar los puertos abiertos en un host sin establecer una conexión completa.&#x20;

Puede realizarse rápidamente, sondeando miles de puertos por segundo en una red rápida en la que no existan cortafuegos. El sondeo SYN es relativamente sigiloso y poco molesto, ya que no llega a completar las conexiones TCP. El escaneo muestra una clara y fiable diferenciación entre los estados `abierto`, `cerrado`, y `filtrado`.

A esta técnica se la conoce habitualmente como sondeo medio abierto, porque no se llega a abrir una conexión TCP completa. Se envía un paquete SYN, como si se fuera a abrir una conexión real y después se espera una respuesta. Si se recibe un paquete SYN/ACK esto indica que el puerto está en escucha (abierto), mientras que si se recibe un RST (reset) indica que no hay nada escuchando en el puerto. Si no se recibe ninguna respuesta después de realizar algunas retransmisiones entonces el puerto se marca como filtrado. También se marca el puerto como filtrado si se recibe un error de tipo ICMP no alcanzable (tipo 3, códigos 1,2, 3, 9, 10, ó 13).

```
nmap -sS 192.168.1.251
```

#### TCP Connect Scan (**-sT**)

```
nmap -sT 192.168.1.251
```

#### UDP Scan (**-sU**)

#### TCP FIN Scan (**-sF**)

#### Host Discovery Scan (**-sn**)

#### Timing Options (**-T 0-5**)
