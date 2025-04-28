# Protección con Fail2Ban

Es una herramienta para proteger tus servidores en Linux contra ataques de fuerza bruta y otros intentos de acceso no autorizado. Mediante el monitoreo de los registros del sistema, Fail2Ban identifica patrones de ataques y toma medidas automáticas para bloquear a las IPs maliciosas, protegiendo así tus servicios.

### Archivos clave de configuración

* **`/etc/fail2ban/fail2ban.conf`**: Configuración general de Fail2Ban.
* **`/etc/fail2ban/jail.conf`**: Archivo de configuración de las "prisiones" (jails), que define qué servicios serán monitoreados.
* **`/etc/fail2ban/jail.d/*.conf`**: Archivos personalizados para la configuración de prisiones adicionales.

### Comandos esenciales

| Comando                                      | Descripción                                                |
| -------------------------------------------- | ---------------------------------------------------------- |
| `sudo systemctl start fail2ban`              | Iniciar Fail2Ban.                                          |
| `sudo systemctl enable fail2ban`             | Habilitar Fail2Ban al arrancar el sistema.                 |
| `sudo systemctl status fail2ban`             | Verificar el estado del servicio Fail2Ban.                 |
| `sudo fail2ban-client status`                | Ver el estado general de Fail2Ban y las prisiones activas. |
| `sudo fail2ban-client status sshd`           | Ver el estado de la prisión SSH.                           |
| `sudo fail2ban-client set sshd unbanip <IP>` | Desbloquear manualmente una IP.                            |
| `sudo fail2ban-client set sshd banip <IP>`   | Bloquear manualmente una IP.                               |

***

### Ejemplo: Configuración básica para SSH

#### Paso 1: Crear archivo de configuración

Crea un archivo en `/etc/fail2ban/jail.d/` para configurar la protección SSH.

```bash
sudo nano /etc/fail2ban/jail.d/ssh.conf
```

#### Paso 2: Definir configuración de la prisión SSH

Agrega las siguientes líneas para configurar la protección SSH:

```bash
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 600
findtime = 600
```

* `enabled = true`: Activar la protección SSH.
* `port = ssh`: Puerto SSH (por defecto 22).
* `filter = sshd`: Usa el filtro predefinido para SSH.
* `logpath = /var/log/auth.log`: Ubicación del log que Fail2Ban monitorea.
* `maxretry = 3`: Número de intentos fallidos permitidos antes de bloquear la IP.
* `bantime = 600`: Tiempo de bloqueo de la IP en segundos (600 segundos = 10 minutos).
* `findtime = 600`: Periodo de tiempo en el que se deben contar los intentos fallidos.

#### Paso 3: Reiniciar Fail2Ban

Para aplicar los cambios, reinicia el servicio Fail2Ban:

```bash
sudo systemctl restart fail2ban
```

#### Paso 4: Verificar el estado

Puedes verificar que el servicio y las prisiones están funcionando correctamente con:

```bash
sudo fail2ban-client status
sudo fail2ban-client status sshd
```

***

### Reglas avanzadas

#### Para bloquear una IP

```bash
sudo fail2ban-client set sshd banip 192.168.1.100
```

#### Desbloquear una IP

```bash
sudo fail2ban-client set sshd unbanip 192.168.1.100
```

#### Ver IPs baneadas

```bash
sudo fail2ban-client status sshd
```

***



#### Mas información

{% embed url="https://www.digitalocean.com/community/tutorials/how-fail2ban-works-to-protect-services-on-a-linux-server" %}

{% @github-files/github-code-block url="https://github.com/fail2ban/fail2ban" %}
