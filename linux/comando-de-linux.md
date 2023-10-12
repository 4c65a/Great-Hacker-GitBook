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

| Comando | descripción                                                                         |
| ------- | ----------------------------------------------------------------------------------- |
| ls      | Listar el contenido del directorio                                                  |
| pwd     | Imprimir el directorio de trabajo                                                   |
| uname   | Imprime la información del sistema operativo                                        |
| arch    | Arquitectura del sistema                                                            |
| cat     | Imprime el contenido del archivo                                                    |
| cd      | Cambiar de directorio                                                               |
| mv      | Mover archivos o carpeta                                                            |
| sudo    | Ejecutar comandos con los privilegios                                               |
| touch   | Crear archivos                                                                      |
| rm      | Eliminar                                                                            |
| whoami  | Nombre de usuario                                                                   |
| date    | Fecha y tiempo                                                                      |
| locate  | Buscar archivos y directorios en el sistema de archivos mas,es mas rapido que find  |
| find    | Buscar archivos y directorios en el sistema de archivos                             |
| mkdir   | Crear directorio                                                                    |
| mrdir   | Eliminar directorio                                                                 |
| Exit    | Salir                                                                               |
| Clear   | Limpiar terminal                                                                    |

### Networks

| Comando                                | Descripción                                                                                               |
| -------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| ip                                     | Para configurar las interfaces de red                                                                     |
| ip addr                                | Imprimir una información en todos los dispositivos de la red                                              |
| ip addr show dev eth0                  | Imprimir una información en el dispositivo _eth0_                                                         |
| ip -4 a                                | Imprimir el protocolo IPv4                                                                                |
| ip -6 a                                | Imprimir el protocolo IPv6                                                                                |
| ip -4 addr show dev eth0               | Mostrar la información relacionada con IPv4 sobre la interfaz de red _eth0_                               |
| ip -6 addr show dev eth0               | Mostrar la información relacionada con IPv4 sobre la interfaz de red _eth0_                               |
| sudo ip addr del 10.0.2.15/24 dev eth0 | Para eliminar la IP _10.0.2.15/24_ de la interfaz de red _eth0_                                           |
| sudo ip addr add 10.0.2.15/24 dev eth0 | Para agregar una dirección IP                                                                             |
| sudo ip link set down eth0             | Para deshabilitar una tarjeta de red (eth0 debe reemplazarse con el nombre correcto de la tarjeta de red) |
| sudo ip link set up eth0               | Para habilitar una tarjeta de red (eth0 debe reemplazarse con el nombre correcto de la tarjeta de red)    |
| ping                                   | Se utiliza para saber si un dispositivo está conectado a una re                                           |
| sudo dhclient eth0                     |                                                                                                           |
|                                        |                                                                                                           |
|                                        |                                                                                                           |
|                                        |                                                                                                           |
|                                        |                                                                                                           |
|                                        |                                                                                                           |
|                                        |                                                                                                           |
