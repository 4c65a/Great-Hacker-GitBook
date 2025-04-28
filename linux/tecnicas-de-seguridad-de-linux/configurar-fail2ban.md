# Fortificación con UFW

Es una **interfaz simplificada** para gestionar reglas de `iptables`, diseñada para facilitar la administración de un firewall básico en sistemas Linux.



***

## **Comandos esenciales de UFW**

| Comando                             | Descripción                                                   |
| ----------------------------------- | ------------------------------------------------------------- |
| `sudo ufw status`                   | Muestra el estado actual del firewall y las reglas aplicadas. |
| `sudo ufw enable`                   | Activa UFW y aplica las reglas.                               |
| `sudo ufw disable`                  | Desactiva UFW, quitando la protección.                        |
| `sudo ufw default deny incoming`    | Bloquea todo tráfico entrante por defecto.                    |
| `sudo ufw default allow outgoing`   | Permite todo tráfico saliente por defecto.                    |
| `sudo ufw allow 22`                 | Permite el puerto 22 (SSH) desde cualquier IP.                |
| `sudo ufw allow from 192.168.1.100` | Permite todo tráfico proveniente de `192.168.1.100`.          |
| `sudo ufw deny 80`                  | Bloquea explícitamente el puerto 80 (HTTP).                   |
| `sudo ufw delete allow 22`          | Elimina la regla que permitía el puerto 22.                   |
| `sudo ufw reload`                   | Recarga las reglas sin desactivar el firewall.                |
| `sudo ufw reset`                    | Resetea todas las reglas y ajustes a su estado original.      |
| `sudo ufw app list`                 | Lista aplicaciones conocidas con perfiles de firewall.        |

***

## **Flujo típico de configuración básica con UFW**

1. Definir políticas por defecto:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

2. Permitir lo esencial (ejemplo: SSH):

```bash
sudo ufw allow 22
```

3. Activar UFW:

```bash
sudo ufw enable
```

4. Verificar las reglas activas:

```bash
sudo ufw status verbose
```

5. Permitir tráfico HTTP y HTTPS:

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

6. Permitir tráfico completo desde una IP específica:

```bash
sudo ufw allow from 192.168.1.100
```

7. Permitir acceso SSH desde una IP específica:

```bash
sudo ufw allow from 192.168.1.100 to any port 22
```

8. Permitir un rango de puertos TCP (ejemplo: 1000–2000):

```bash
sudo ufw allow 1000:2000/tcp
```

9. Bloquear una IP específica:

```bash
sudo ufw deny from 203.0.113.45
```

10. Bloquear tráfico de una IP en una interfaz específica (ejemplo: eth0):

```bash
sudo ufw deny in on eth0 from 203.0.113.45
```

11. Ver listado numerado de reglas:

```bash
sudo ufw status numbered
```

12. Eliminar una regla específica (usando su número):

```bash
sudo ufw delete 0
```

13. Habilitar el registro de eventos de UFW:

```bash
sudo ufw logging on
```

14. Deshabilitar el registro de eventos:

```bash
sudo ufw logging off
```

15. Listar perfiles de aplicaciones disponibles:

```bash
sudo ufw app list
```

***

{% hint style="success" %}
**También existe la version grafica GUFW**
{% endhint %}

#### Para mas información

{% embed url="https://help.ubuntu.com/community/UFW" %}
