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

# Escaneo de puertos con nmap

**Nmap** (escrito por Gordon Lyon, también conocido como Fyodor) es uno de los escáneres de puertos más populares, versátiles y robustos disponibles. Se ha desarrollado activamente durante más de dos décadas y ofrece numerosas funciones más allá del escaneo de puertos.

**Algunos de los ejemplos de escaneo de Nmap que cubriremos en este módulo se ejecutan utilizando sudo. Esto se debe a que bastantes opciones de escaneo de Nmap requieren acceso a sockets raw,** que a su vez requieren privilegios de root. Los sockets raw permiten la manipulación quirúrgica de paquetes TCP y UDP. Sin acceso a sockets raw, Nmap está limitado, ya que recurre a la creación de paquetes utilizando la API estándar de sockets Berkeley.\*\*

**Antes de explorar algunos ejemplos de escaneo de puertos, debemos comprender la huella que cada escaneo de Nmap deja en la red y los hosts escaneados.**

**Un escaneo TCP predeterminado de Nmap escaneará los 1000 puertos más populares en una máquina determinada. Antes de comenzar a ejecutar escaneos a ciegas, examinemos la cantidad de tráfico enviado por este tipo de escaneo. Escanearemos una de las máquinas del laboratorio mientras monitoreamos la cantidad de tráfico enviado al host objetivo usando iptables.**

**Utilizaremos varias opciones de iptables. Primero, usemos la opción -I para insertar una nueva regla en una cadena determinada, que en este caso incluye tanto la cadena INPUT (entrada) como la OUTPUT (salida), seguida del número de regla. Podemos usar -s para especificar una dirección IP de origen, -d para especificar una dirección IP de destino y -j para ACCEPTAR el tráfico. Finalmente, usaremos la opción -Z para poner a cero los contadores de paquetes y bytes en todas las cadenas.**

```
kali@kali:~$ sudo iptables -I INPUT 1 -s 192.168.50.149 -j ACCEPT
kali@kali:~$ sudo iptables -I OUTPUT 1 -d 192.168.50.149 -j ACCEPT
```

