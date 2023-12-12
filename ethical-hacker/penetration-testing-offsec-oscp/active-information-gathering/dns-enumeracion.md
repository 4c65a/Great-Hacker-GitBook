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

# DNS Enumeracion

El Sistema de Nombres de Dominio DNS es una base de datos distribuida responsable de traducir nombres de dominio fáciles de recordar para los usuarios en direcciones IP.&#x20;

Esto se facilita mediante una estructura jerárquica dividida en varias zonas, comenzando por la zona raíz de nivel superior.

Cada dominio puede utilizar diferentes tipos de registros DNS. Algunos de los tipos de registros DNS más comunes son:

* **NS:** Los registros de servidor de nombres contienen el nombre de los servidores autorizados que alojan los registros DNS de un dominio.
* **A:** También conocido como registro de host, el "registro A" contiene la dirección IPv4 de un nombre de host.
* **AAAA:** También conocido como registro de host cuádruple A, el "registro AAAA" contiene la dirección IPv6 de un nombre de host.
* **MX:** Los registros de intercambio de correo electrónico contienen los nombres de los servidores responsables de manejar el correo electrónico del dominio. Un dominio puede contener varios registros MX.
* **PTR:** Los registros de puntero se utilizan en zonas de búsqueda inversa y pueden encontrar los registros asociados con una dirección IP.
* **CNAME:** Los registros de nombre canónico se utilizan para crear alias para otros registros de host.
* **TXT:** Los registros TXT pueden contener cualquier dato arbitrario y utilizarse para diversos fines, como la verificación de la propiedad del dominio.

Debido a la gran cantidad de información contenida en el DNS, suele ser un objetivo lucrativo para la recopilación activa de información.

Demostremos esto usando el comando `host` para encontrar la dirección IP.

```
host www.example.com
www.example.com has address 149.56.244.87
```

El comando `host` busca por defecto un registro A, pero también podemos consultar otros campos, como registros MX o TXT, especificando el tipo de registro en nuestra consulta usando la opción `-t`.

```
host -t mx example.com
```

En este caso, primero ejecutamos el comando `host` para obtener solo los registros MX.

Ejecutamos el comando `host` nuevamente para recuperar solo los registros TXT.

```
host -t txt example.com
```

Podemos continuar usando consultas DNS adicionales para descubrir más nombres de host y direcciones IP que pertenecen al mismo dominio.

Ejecutemos `host` contra este nombre de host.

```
host www.example.com
www.example.com has address 149.56.244.87
```

Consultamos un nombre de host válido y recibimos una respuesta de resolución de IP.&#x20;

La fuerza bruta es una técnica de prueba y error que busca encontrar información válida, como directorios en un servidor web, combinaciones de nombre de usuario y contraseña o, en este caso, registros DNS válidos. Mediante el uso de una lista de palabras que contiene nombres de host comunes, podemos intentar adivinar registros DNS y verificar la respuesta de los nombres de host válidos.

Utilizamos búsquedas directas, que solicitan la dirección IP de un nombre de host para consultar tanto un nombre de host válido como uno no válido. Si el host resuelve con éxito un nombre a una IP, esto podría ser una indicación de un servidor funcional.

Creamos una lista de posibles nombres de host.

{% code title="list.txt" %}
```
www
ftp
mail
owa
proxy
router
no
```
{% endcode %}

A continuación, podemos usar una línea de comandos de Bash para intentar resolver cada nombre de host.

```
for ip in $(cat list.txt); do host $ip.example.com; done
www.example.com has address 149.56.244.87
Host ftp.example.com not found: 3(NXDOMAIN)
mail.v.com has address 51.222.169.212
Host owa.example.com not found: 3(NXDOMAIN)
Host proxy.example.com not found: 3(NXDOMAIN)
router.vcom has address 51.222.169.214
```

Utilizando esta lista de palabras simplificada, descubrimos entradas para "www", "mail" y "router". Sin embargo, los nombres de host "ftp", "owa" y "proxy" no se encontraron.&#x20;

Con la excepción del registro www, nuestra enumeración de fuerza bruta hacia adelante de DNS reveló un conjunto de direcciones IP dispersas en el mismo rango aproximado (51.222.169.X).&#x20;

Si el administrador de DNS de example.com configuró registros PTR para el dominio, podríamos escanear el rango aproximado con búsquedas inversas para solicitar el nombre de host de cada IP.

Usemos un bucle para escanear las direcciones IP 51.222.169.200 a 51.222.169.254. Filtraremos los resultados no válidos (usando grep -v) mostrando solo las entradas que no contienen "no encontrado".

```
for ip in $(seq 200 254); do host 51.222.169.$ip; done | grep -v "not found"
...
208.169.222.51.in-addr.arpa domain name pointer admin.example.com.
209.169.222.51.in-addr.arpa domain name pointer beta.example.com.
210.169.222.51.in-addr.arpa domain name pointer fs1.example.com.
211.169.222.51.in-addr.arpa domain name pointer intranet.example.com.
212.169.222.51.in-addr.arpa domain name pointer mail.example.com.
213.169.222.51.in-addr.arpa domain name pointer mail2.example.com.
214.169.222.51.in-addr.arpa domain name pointer router.example.com.
215.169.222.51.in-addr.arpa domain name pointer siem.example.com.
216.169.222.51.in-addr.arpa domain name pointer snmp.example.com.
217.169.222.51.in-addr.arpa domain name pointer syslog.example.com.
218.169.222.51.in-addr.arpa domain name pointer support.example.com.
219.169.222.51.in-addr.arpa domain name pointer test.example.com.
220.169.222.51.in-addr.arpa domain name pointer vpn.example.com.
...
```

Hemos logrado resolver con éxito una serie de direcciones IP a hosts válidos utilizando búsquedas inversas de DNS. Si estuviéramos realizando una evaluación, podríamos extrapolar aún más estos resultados y analizar "mail2", "router", y realizar una búsqueda inversa de los resultados positivos. Este tipo de escaneos suelen ser cíclicos.

DNSRecon es un script avanzado de enumeración de DNS escrito en Python,usando la opción `-d` para especificar un nombre de dominio y `-t` para especificar el tipo de enumeración a realizar .

```
dnsrecon -d example.com -t std
```

Ahora intentemos forzar la búsqueda de nombres de host adicionales utilizando el archivo list.txt que creamos previamente para búsquedas directas.

```
list.txt
www
ftp
mail
owa
proxy
router
```

Para realizar nuestro intento de fuerza bruta, utilizaremos la opción `-d` para especificar un nombre de dominio, `-D` para especificar un nombre de archivo que contenga posibles cadenas de subdominio y `-t` para especificar el tipo de enumeración a realizar, en este caso `brt` para fuerza bruta.

```
dnsrecon -d example.com -D ~/list.txt -t brt
```

DNSEnum es otra herramienta popular de enumeración de DNS .

```
dnsenum example.com
```

Exploremos qué tipo de enumeración de DNS podemos realizar desde una perspectiva de Windows.

Podemos ejecutar una consulta simple para resolver el registro A del host `mail.example.com`.

```
nslookup mail.example.com
La solicitud de DNS ha expirado.
El tiempo de espera fue de 2 segundos.
Servidor: Desconocido
Dirección: 192.168.50.151
Nombre:
mail.example.com
Dirección: 192.168.50.154
```

De manera similar al comando `host` de Linux, `nslookup` puede realizar consultas más granulares. Podemos consultar un DNS determinado sobre un registro TXT que pertenece a un host específico.

```
nslookup -type=TXT info.example.com 192.168.50.151
Servidor: Desconocido
Dirección: 192.168.50.151
```
