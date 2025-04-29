# Aislamiento con AppArmor

**AppArmor** (Application Armor) es un módulo de seguridad para el kernel de Linux que aplica control de acceso obligatorio (MAC) mediante perfiles que restringen lo que cada programa puede hacer.\
Permite aislar procesos, limitar su alcance y proteger el sistema incluso si una aplicación es comprometida.

***

### Comandos Básicos

| Comando                                | Descripción                            |
| -------------------------------------- | -------------------------------------- |
| `sudo systemctl status apparmor`       | Verificar si AppArmor está activo      |
| `sudo aa-status`                       | Mostrar perfiles cargados y sus modos  |
| `sudo aa-enforce /ruta/perfil`         | Activar modo de refuerzo (bloqueo)     |
| `sudo aa-complain /ruta/perfil`        | Activar modo permisivo (solo registro) |
| `sudo apparmor_parser -r /ruta/perfil` | Recargar perfil tras editarlo          |
| `sudo aa-disable /ruta/perfil`         | Desactivar un perfil                   |

***

### Flujo Básico de Uso

1. Verificar estado:

```bash
sudo systemctl status apparmor
```

2. Ver perfiles activos:

```bash
sudo aa-status
```

3. Aplicar modo de refuerzo a un perfil:

```bash
sudo aa-enforce /etc/apparmor.d/usr.sbin.sshd
```

4. Cambiar a modo permisivo:

```bash
sudo aa-complain /etc/apparmor.d/usr.sbin.sshd
```

5. Crear un perfil automáticamente:

```bash
sudo aa-genprof nginx
```

6. Recargar tras edición manual:

```bash
sudo apparmor_parser -r /etc/apparmor.d/usr.sbin.sshd
```

7. Desactivar un perfil:

```bash
sudo aa-disable /etc/apparmor.d/usr.sbin.sshd
```

***

### Perfiles y Ubicación

Todos los perfiles están en:

```bash
/etc/apparmor.d/
```

Ejemplos:

* `usr.sbin.sshd` — Servidor SSH
* `usr.bin.dnsmasq` — DNSMasq
* `usr.sbin.nginx` — Nginx

***

### Modos de Operación

* **enforce**: Bloquea acciones no permitidas.
* **complain**: Solo registra violaciones (útil para pruebas).
* **disable**: Perfil no se aplica.

***

### Caso Práctico: Proteger SSH

```bash
sudo aa-enforce /etc/apparmor.d/usr.sbin.sshd
sudo aa-status
```

Deberías ver `sshd` en modo `enforce`.

***

