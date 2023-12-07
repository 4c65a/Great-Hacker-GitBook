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

# Comando de Linux

### Básicos

| Comando  | descripción                                                                         |
| -------- | ----------------------------------------------------------------------------------- |
| ls       | Listar el contenido del directorio                                                  |
| pwd      | Imprimir el directorio de trabajo                                                   |
| uname    | Imprime la información del sistema operativo                                        |
| arch     | Arquitectura del sistema                                                            |
| cat      | Imprime el contenido del archivo                                                    |
| cd       | Cambiar de directorio                                                               |
| mv       | Mover archivos o carpeta                                                            |
| sudo     | Ejecutar comandos con los privilegios                                               |
| touch    | Crear archivos                                                                      |
| rm       | Eliminar                                                                            |
| whoami   | Nombre de usuario                                                                   |
| date     | Fecha y tiempo                                                                      |
| locate   | Buscar archivos y directorios en el sistema de archivos mas,es mas rapido que find  |
| find     | Buscar archivos y directorios en el sistema de archivos                             |
| mkdir    | Crear directorio                                                                    |
| mrdir    | Eliminar directorio                                                                 |
| exit     | Salir                                                                               |
| clear    | Limpiar terminal                                                                    |
| shred -u | Eliminar de manera segura archivos y directorios,-u indica que debe eliminarse      |

### Networks

| Comando                           | Descripción                                                                                                                                        |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| ip                                | Para configurar las interfaces de red                                                                                                              |
| ip addr                           | Imprimir una información en todos los dispositivos de la red                                                                                       |
| ip addr show dev eth0             | Imprimir una información en el dispositivo _eth0_                                                                                                  |
| ip -4 a                           | Imprimir el protocolo IPv4                                                                                                                         |
| ip -6 a                           | Imprimir el protocolo IPv6                                                                                                                         |
| ip -4 addr show dev eth0          | Mostrar la información relacionada con IPv4 sobre la interfaz de red _eth0_                                                                        |
| ip -6 addr show dev eth0          | Mostrar la información relacionada con IPv4 sobre la interfaz de red _eth0_                                                                        |
| ip addr del 10.0.2.15/24 dev eth0 | Para eliminar la IP _10.0.2.15/24_ de la interfaz de red _eth0_                                                                                    |
| ip addr add 10.0.2.15/24 dev eth0 | Para agregar una dirección IP                                                                                                                      |
| ip link set down eth0             | Para deshabilitar una tarjeta de red (eth0 debe reemplazarse con el nombre correcto de la tarjeta de red)                                          |
| ip link set up eth0               | Para habilitar una tarjeta de red (eth0 debe reemplazarse con el nombre correcto de la tarjeta de red)                                             |
| ping                              | Se utiliza para saber si un dispositivo está conectado a una re                                                                                    |
| dhclient eth0                     | asignará una dirección IP a la interfaz de red eth0                                                                                                |
| host                              | Permite conocer la dirección IP de un nombre de dominio (También se puede agregar la ip)                                                           |
| hostname                          | Permite editar el nombre de host de su sistema(solo hasta el reinicio)                                                                             |
| iwconfig                          | Muestra configuraciones                                                                                                                            |
| ifconfig                          | Muestra configuraciones                                                                                                                            |
| ip route                          | Muestra las puertas de enlace configuradas(ip r)                                                                                                   |
| ip route add default via x.x.x.x  | Se puede agregar una puerta de enlace predeterminada para acceder a la red                                                                         |
| ip route add prohibit x.x.x.x     | Para bloquear una puerta de enlace predeterminada(ip de la computadora)                                                                            |
| ip route delete default           | Para eliminarla                                                                                                                                    |
| traceroute                        | Identificar la ruta que toman los paquetes para llegar al host                                                                                     |
| ss                                | Obtiene detalles sobre los sockets de red                                                                                                          |
| dig                               | Proporciona toda la información necesaria sobre el servidor de nombres DNS                                                                         |
| curl                              | Transfiere datos a través de la red al admitir varios protocolos                                                                                   |
| nslookup google.com               | Para consultar DNS para obtener un nombre de dominio(se puede usar una IP)                                                                         |
| arp                               | Se utiliza para manipular la tabla ARP del kernel. Con este comando, puede ver, agregar, actualizar o eliminar entradas en la tabla ARP del kernel |
| wget                              | Se utiliza para descargar archivos mediante protocolos HTTP, HTTPS, FTP                                                                            |
| netstat                           | utiliza para examinar las conexiones de red, las tablas de enrutamiento y diversas configuraciones y estadísticas de red                           |
| netstat -napt                     | Saber qué puertos tiene abiertos nuestro sistema                                                                                                   |
| netstat -n                        | No resuelve las direcciones a sus nombres DNS                                                                                                      |
| netstat -a                        | Muestra todas las conexiones                                                                                                                       |
| netstat -p                        | Muestra el número y nombre del dueño de dicha conexión                                                                                             |
| netstat -t                        | Sólo muestra conexiones tcp                                                                                                                        |
| traceroute -4                     | Rastrea la ruta a una dirección IP IPv4                                                                                                            |
| traceroute -6                     | Rastrea la ruta a una dirección IP IPv6                                                                                                            |
| traceroute -4 -m 5                | Limitar el número de saltos                                                                                                                        |
| traceroute -i eth0                | Especificar la interfaz de red                                                                                                                     |
| traceroute -r                     | Evitar que el comando use las cachés de resolución de nombres                                                                                      |
| traceroute -s 60                  | Especificar el tamaño del paquete                                                                                                                  |
| traceroute -w 100                 | Establecer el tiempo de espera para cada salto en mili segundos                                                                                    |
| whois                             | Informacion detallada del dominio                                                                                                                  |



