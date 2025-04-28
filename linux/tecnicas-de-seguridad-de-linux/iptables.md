# Fortificación con iptables

Esta herramienta es fundamental para la gestión del tráfico de red en sistemas Linux. Permite establecer una tabla de reglas que determinan qué conexiones se aceptan, se rechazan o se bloquean, formando el muro de defensa de nuestro sistema.

***

## Configuración Básica

La primera tarea para fortificar un sistema Linux es establecer políticas estrictas con iptables. Procedemos de inmediato a verificar el estado actual y a aplicar las primeras reglas defensivas.

### Verificar instalación de iptables

Antes de aplicar cualquier regla, es necesario comprobar que iptables está operativo en el sistema:

<pre class="language-bash"><code class="lang-bash"><strong>sudo iptables -L
</strong></code></pre>

Este comando lista todas las reglas activas. Si no muestra errores, iptables está instalado y funcionando.

***

### Establecer políticas por defecto seguras

Todo tráfico que no esté explícitamente permitido debe ser rechazado por defecto. Ejecuta:

```bash
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP
sudo iptables -P OUTPUT ACCEPT
```

* **INPUT DROP**: Todo tráfico entrante es bloqueado si no se permite explícitamente.
* **FORWARD DROP**: No se permite redireccionamiento de paquetes.
* **OUTPUT ACCEPT**: Se permite todo tráfico saliente desde la máquina.

Estas políticas reflejan la estrategia de **cierre total**: solo permitimos puertas que nosotros mismos abrimos.

***

### Permitir tráfico esencial

Ciertos flujos deben ser aceptados para no aislar completamente el sistema:

1. Permitir conexiones ya establecidas y relacionadas:

```bash
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

Esto garantiza que las respuestas legítimas a conexiones salientes (como navegación web) sean aceptadas.

2. Permitir el tráfico del loopback:

```bash
sudo iptables -A INPUT -i lo -j ACCEPT
```

Esto asegura que los procesos internos del sistema puedan comunicarse entre sí.

***

### Permitir trafico de un puerto en especifico

Estos comandos permite aceptar el trafico en determinado puertos.

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

```bash
sudo iptables -A INPUT -p udp --dport 137 -j ACCEPT
```

***

### Permitir trafico de una dirección ip en especifico

Para aceptar el trafico de determinada IP.

```bash
sudo iptables -A INPUT -s 192.168.1.100 -j ACCEPT
```

Bloquear el trafico de una dirección IP.

```bash
sudo iptables -A INPUT -s 192.168.1.111 -j DROP
```

Rechazar trafico de un determinado rango de IP.

```bash
sudo iptables -A INPUT -m iprange --src-range 192.168.1.100-192.168.1.200 -j REJECT
```

***

### Eliminar las configuraciones

Para listar la regla.

```bash
sudo iptables -L --line-numbers
```

Para eliminar una regla existente.

```bash
sudo iptables -D INPUT 1
```

***

