# Fortificación con UFW

Es una **interfaz simplificada** para gestionar reglas de `iptables`, diseñada para facilitar la administración de un firewall básico en sistemas Linux.\
No reemplaza a `iptables`, sino que **lo configura automáticamente** siguiendo tus órdenes.



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
| `sudo ufw allow "Nginx Full"`       | Permite puertos requeridos por una app (ej: nginx).           |

***

## **Flujo típico de configuración básica con UFW**

1.  **Definir políticas por defecto:**

    ```bash
    sudo ufw default deny incoming
    sudo ufw default allow outgoing
    ```
2.  **Permitir lo esencial (ej: SSH):**

    ```bash
    sudo ufw allow 22 
    ```
3.  **Activar UFW:**

    ```bash
    sudo ufw enable
    ```
4.  **Verificar reglas:**

    ```bash
    sudo ufw status verbose
    ```

***



