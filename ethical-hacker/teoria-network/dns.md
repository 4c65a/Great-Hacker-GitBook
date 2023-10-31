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

# DNS

En las redes de datos, los dispositivos se etiquetan con direcciones IP.Los nombres de dominio se crearon para convertir las direcciones numéricas en un nombre sencillo y reconocible .Los DNS o llamado el sistema de nombres de dominios ([The Domain Name System](https://www.cloudflare.com/learning/dns/what-is-dns/)),lo que hace es asignarle un nombre o apodo a una dirección IP,por defecto este tiene el puerto 53.

Los DNS traducen una ip para que las persona se puedan acordad del nombre de la pagina mas fácil ,por ejemplo, www.amazon.com a direcciones IP aptas para lectura por parte de máquinas 192.0.255.102.

El protocolo DNS define un servicio automatizado que coincide con nombres de recursos que tienen la dirección de red numérica solicitada. Incluye el formato de consultas, respuestas y datos. Las comunicaciones del protocolo DNS utilizan un único formato llamado “mensaje”. Este formato de mensaje se utiliza para todos los tipos de solicitudes de clientes y respuestas del servidor, mensajes de error y para la transferencia de información de registro de recursos entre servidores.

### Zone transfer

Es una técnica de reconocimiento que se utiliza para obtener una copia de la zona DNS de un dominio. La zona DNS contiene información sobre los [registros DNS](https://www.cloudflare.com/es-es/learning/dns/dns-records/) del dominio.

| Registro | Significado                                                                                                                                              |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A        | registro que contiene la dirección IP de un dominio.                                                                                                     |
| AAAA     | El registro que contiene la dirección IPv6 de un dominio (a diferencia de los registros A, que enumeran la dirección IPv4).                              |
| CNAME    | reenvía un dominio o subdominio a otro dominio, NO proporciona una dirección IP.                                                                         |
| MX       | dirige el correo a un servidor de correo electrónico.                                                                                                    |
| TXT      | Permite que un administrador pueda almacenar notas de texto en el registro. Estos registros se suelen utilizar para la seguridad del correo electrónico. |
| NS       | almacena el servidor de nombres para una entrada DNS                                                                                                     |
| SOA      | almacena la información del administrador sobre un dominio                                                                                               |
| SRV      | especifica un puerto para servicios específicos                                                                                                          |
| PTR      | proporciona un nombre de dominio en búsquedas inversas.                                                                                                  |

Si el servidor de nombres permite que se produzcan transferencias de zona por parte de un usuario anónimo, se devolverán todos los nombres DNS y direcciones IP alojados por el servidor de nombres en texto ASCII legible por humanos



#### Referencias

{% embed url="https://skillsforall.com/course/networking-devices-and-initial-configuration?courseLang=en-US" %}
