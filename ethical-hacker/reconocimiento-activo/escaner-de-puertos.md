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

### Escanear puerto con nmap

Un escaneo de puertos es un escaneo activo en el que la herramienta de escaneo envía varios tipos de sondas a la dirección IP de destino y luego examina las respuestas para determinar si el servicio está realmente escuchando. Por ejemplo, con un escaneo SYN de Nmap, la herramienta envía un paquete SYN TCP al puerto TCP que está sondeando. Este proceso también se conoce como escaneo semiabierto porque no abre una conexión TCP completa.

Si la respuesta es un SYN/ACK, esto indicaría que el puerto está realmente en un estado de escucha. Si la respuesta al paquete SYN es un RST (reset), esto indicaría que el puerto está cerrado o no está en un estado de escucha. Si la sonda SYN no recibe respuesta, Nmap lo marca como filtrado porque no puede determinar si el puerto está abierto o cerrado.



```
nmap -sS 192.168.88.251
```
