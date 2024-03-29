# Enumeración

**hostname**

El comando hostname devolverá el nombre de host de la máquina objetivo.

**uname -a**

Imprimirá información del sistema dándonos detalles adicionales sobre el kernel utilizado por el sistema.

**/proc/version**

El sistema de archivos proc (procfs) proporciona información sobre los procesos del sistema objetivo.&#x20;

**/etc/issue**

Los sistemas también pueden ser identificados al mirar el archivo /etc/issue. Este archivo generalmente contiene alguna información sobre el sistema operativo pero puede ser personalizado o cambiado fácilmente.

**ps**

El comando ps es una forma efectiva de ver los procesos en ejecución en un sistema Linux. Escribir ps en tu terminal mostrará los procesos para el shell actual.&#x20;

```yaml
PID: El ID del proceso (único para el proceso)
TTY: Tipo de terminal utilizado por el usuario
Tiempo: Cantidad de tiempo de CPU utilizado por el proceso (esto NO es el tiempo que ha estado en ejecución este proceso)
CMD: El comando o ejecutable en ejecución (NO mostrará ningún parámetro de línea de comando)
```

**env**

El comando env mostrará variables de entorno.

**sudo -l**

El sistema objetivo puede estar configurado para permitir que los usuarios ejecuten algunos (o todos) los comandos con privilegios de root. El comando sudo -l se puede usar para enumerar todos los comandos que tu usuario puede ejecutar usando sudo.

**id**

El comando id proporcionará una visión general del nivel de privilegio del usuario y de las membresías en grupos.

**/etc/passwd**

Leer el archivo /etc/passwd puede ser una forma fácil de descubrir usuarios en el sistema.

Otro enfoque podría ser buscar "home" ya que los usuarios reales probablemente tengan sus carpetas bajo el directorio "home".

**history**

Mirar comandos anteriores con el comando history puede darnos una idea sobre el sistema objetivo y, aunque raramente, tener información almacenada como contraseñas o nombres de usuario.

**ifconfig**

El sistema objetivo puede ser un punto de pivote hacia otra red. El comando ifconfig nos dará información sobre las interfaces de red del sistema.

**netstat**

El comando netstat se puede usar con varias opciones diferentes para recopilar información sobre las conexiones existentes.

```java
netstat -a: muestra todos los puertos de escucha y las conexiones establecidas.
netstat -at o netstat -au también se pueden usar para listar protocolos TCP o UDP respectivamente.
netstat -l: lista puertos en modo de "escucha". Estos puertos están abiertos y listos para aceptar conexiones entrantes. Esto se puede usar con la opción "t" para listar solo puertos que están escuchando utilizando el protocolo TCP (abajo)

netstat -s: lista estadísticas de uso de red por protocolo (abajo) Esto también se puede usar con las opciones -t o -u para limitar la salida a un protocolo específico.

netstat -tp: lista conexiones con el nombre del servicio e información del PID.
```

Esto también se puede usar con la opción -l para listar puertos de escucha.

**find**

Buscar en el sistema objetivo información importante y posibles vectores de escalada de privilegios puede ser fructífero. El comando "find" integrado es útil y vale la pena mantenerlo en tu arsenal.

**Carpetas y archivos que se pueden escribir o ejecutar desde:**

```typescript
find / -writable -type d 2>/dev/null: 
find / -perm -222 -type d 2>/dev/null:
find / -perm -o w -type d 2>/dev/null:
```

```typescript
find / -perm -o x -type d 2>/dev/null: 
```

**Buscar herramientas de desarrollo y lenguajes compatibles:**

```arduino
find / -name perl*
find / -name python*
find / -name gcc*
```

**Buscar permisos de archivo específicos:**

Encontrar archivos con el bit SUID, lo que nos permite ejecutar el archivo con un nivel de privilegio más alto que el usuario actual.

```typescript
find / -perm -u=s -type f 2>/dev/null:
```
