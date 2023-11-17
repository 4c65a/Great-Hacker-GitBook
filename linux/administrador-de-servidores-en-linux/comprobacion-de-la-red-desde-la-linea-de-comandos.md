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

# Comprobación de la red desde la línea de comandos

## Mostrar interfaz de red

Este comando proporciona detalles como las direcciones IP asociadas a cada interfaz, el estado de la interfaz (si está activa o inactiva), la dirección MAC (Media Access Control), y otra información relevante para la configuración y gestión de las conexiones de red.

```bash
ip addr show
```

`ifconfig` muestra información similar a la proporcionada por "ip addr". Sin embargo, "ifconfig" también presenta el número de paquetes recibidos (RX) y transmitidos (TX), junto con la cantidad de datos, y cualquier error o paquete descartado. Este comando es útil para obtener detalles más específicos sobre la actividad de red, como la cantidad de datos transferidos y posibles problemas de conexión.

```bash
ifconfig
```

### Comprobación de la conectividad con sistemas remotos

`ping` es una utilidad de red utilizada para probar la conectividad entre dos dispositivos a través de una red IP. Básicamente, envía paquetes de datos a una dirección específica (ya sea una dirección IP o un nombre de host) y espera a recibir una respuesta. Esto permite verificar si un dispositivo remoto está accesible y mide el tiempo que tarda en recibir una respuesta.

```bash
ping
```

### Comprobación de la información de enrutamiento

`route` permite ver y configurar cómo un sistema operativo dirige el tráfico de red. Puede mostrar la tabla de enrutamiento actual, agregar nuevas rutas, eliminar rutas existentes y realizar otras operaciones relacionadas con el enrutamiento de paquetes.

```bash
route
```

`traceroute` proporciona información valiosa sobre la ruta y los tiempos de respuesta a lo largo del camino que sigue un paquete desde el origen hasta su destino. Es una herramienta útil para diagnosticar problemas de red y entender la topología de la red entre dos puntos.

```bash
traceroute google.com
```

### Comprobar host y nombre de dominio

```bash
hostname
```

```bash
dnsdomainname
```
