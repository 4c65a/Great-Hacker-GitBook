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

El Sistema de Nombres de Dominio (DNS)246 es una base de datos distribuida responsable de traducir nombres de dominio fáciles de recordar para los usuarios en direcciones IP. Es uno de los sistemas más críticos de internet.

Esto se facilita mediante una estructura jerárquica dividida en varias zonas, comenzando por la zona raíz de nivel superior.

Cada dominio puede utilizar diferentes tipos de registros DNS. Algunos de los tipos de registros DNS más comunes son:

* **NS:** Los registros de servidor de nombres contienen el nombre de los servidores autorizados que alojan los registros DNS de un dominio.
* **A:** También conocido como registro de host, el "registro A" contiene la dirección IPv4 de un nombre de host (como [www.megacorpone.com](https://www.megacorpone.com/)).
* **AAAA:** También conocido como registro de host cuádruple A, el "registro AAAA" contiene la dirección IPv6 de un nombre de host (como [www.megacorpone.com](https://www.megacorpone.com/)).
* **MX:** Los registros de intercambio de correo electrónico contienen los nombres de los servidores responsables de manejar el correo electrónico del dominio. Un dominio puede contener varios registros MX.
* **PTR:** Los registros de puntero se utilizan en zonas de búsqueda inversa y pueden encontrar los registros asociados con una dirección IP.
* **CNAME:** Los registros de nombre canónico se utilizan para crear alias para otros registros de host.
* **TXT:** Los registros TXT pueden contener cualquier dato arbitrario y utilizarse para diversos fines, como la verificación de la propiedad del dominio.

Debido a la gran cantidad de información contenida en el DNS, suele ser un objetivo lucrativo para la recopilación activa de información.

Demostremos esto usando el comando `host` para encontrar la dirección IP de [www.megacorpone.com](https://www.megacorpone.com/).

```
kali@kali:~$ host www.megacorpone.com
www.megacorpone.com has address 149.56.244.87
```

El comando `host` busca por defecto un registro A, pero también podemos consultar otros campos, como registros MX o TXT, especificando el tipo de registro en nuestra consulta usando la opción `-t`.

```
kali@kali:~$ host -t mx megacorpone.com
megacorpone.com mail is handled by 10 fb.mail.gandi.net.
megacorpone.com mail is handled by 20 spool.mail.gandi.net.
megacorpone.com mail is handled by 50 mail.megacorpone.com.
megacorpone.com mail is handled by 60 mail2.megacorpone.com.
```

En este caso, primero ejecutamos el comando `host` para obtener solo los registros MX de megacorpone.com, lo que devolvió cuatro registros de servidores de correo diferentes. Cada servidor tiene una prioridad diferente (10, 20, 50, 60) y el servidor con el número de prioridad más bajo se usará primero para reenviar el correo dirigido al dominio megacorpone.com (fb.mail.gandi.net).

Luego, ejecutamos el comando `host` nuevamente para recuperar solo los registros TXT de megacorpone.com, que devolvió dos entradas.

```
kali@kali:~$ host -t txt megacorpone.com
megacorpone.com descriptive text "Try Harder"
megacorpone.com descriptive text "google-site-
verification=U7B_b0HNeBtY4qYGQZNsEYXfCJ32hMNV3GtC0wWq5pA"
```

Ahora que hemos recopilado algunos datos iniciales del dominio megacorpone.com, podemos continuar usando consultas DNS adicionales para descubrir más nombres de host y direcciones IP que pertenecen al mismo dominio.

Por ejemplo, sabemos que el dominio tiene un servidor web con el nombre de host "[www.megacorpone.com](https://www.megacorpone.com/)".

Ejecutemos `host` contra este nombre de host.

```
kali@kali:~$ host www.megacorpone.com
www.megacorpone.com has address 149.56.244.87
```

Ahora, determinemos si megacorpone.com tiene un servidor con el nombre de host "idontexist". Observaremos la diferencia entre las salidas de la consulta.

```
kali@kali:~$ host idontexist.megacorpone.com
Host idontexist.megacorpone.com not found: 3(NXDOMAIN)
```

En el Listado 41, consultamos un nombre de host válido y recibimos una respuesta de resolución de IP. Por el contrario, el Listado 42 devolvió un error (NXDOMAIN247) indicando que no existe un registro DNS público para ese nombre de host. Como ahora comprendemos cómo buscar nombres de host válidos, podemos automatizar nuestros esfuerzos.

Una vez aprendidos los conceptos básicos de enumeración de DNS, podemos desarrollar técnicas de fuerza bruta de DNS para acelerar nuestra investigación.

La fuerza bruta es una técnica de prueba y error que busca encontrar información válida, como directorios en un servidor web, combinaciones de nombre de usuario y contraseña o, en este caso, registros DNS válidos. Mediante el uso de una lista de palabras que contiene nombres de host comunes, podemos intentar adivinar registros DNS y verificar la respuesta de los nombres de host válidos.

En los ejemplos anteriores, utilizamos búsquedas directas, que solicitan la dirección IP de un nombre de host para consultar tanto un nombre de host válido como uno no válido. Si el host resuelve con éxito un nombre a una IP, esto podría ser una indicación de un servidor funcional.

```
kali@kali:~$ cat list.txt
www
ftp
mail
owa
proxy
router
no
```

Primero, creamos una lista de posibles nombres de host.

```
kali@kali:~$ for ip in $(cat list.txt); do host $ip.megacorpone.com; done
www.megacorpone.com has address 149.56.244.87
Host ftp.megacorpone.com not found: 3(NXDOMAIN)
mail.megacorpone.com has address 51.222.169.212
Host owa.megacorpone.com not found: 3(NXDOMAIN)
Host proxy.megacorpone.com not found: 3(NXDOMAIN)
router.megacorpone.com has address 51.222.169.214
```

A continuación, podemos usar una línea de comandos de Bash para intentar resolver cada nombre de host.

```
kali@kali:~$ for ip in $(cat list.txt); do host $ip.megacorpone.com; done
www.megacorpone.com has address 149.56.244.87
Host ftp.megacorpone.com not found: 3(NXDOMAIN)
mail.megacorpone.com has address 51.222.169.212
Host owa.megacorpone.com not found: 3(NXDOMAIN)
Host proxy.megacorpone.com not found: 3(NXDOMAIN)
router.megacorpone.com has address 51.222.169.214
```

Utilizando esta lista de palabras simplificada, descubrimos entradas para "www", "mail" y "router". Sin embargo, los nombres de host "ftp", "owa" y "proxy" no se encontraron. Existen listas de palabras mucho más completas como parte del proyecto SecLists.248 Estas listas de palabras se pueden instalar en el directorio /usr/share/seclists usando el comando sudo apt install seclists.

Con la excepción del registro www, nuestra enumeración de fuerza bruta hacia adelante de DNS reveló un conjunto de direcciones IP dispersas en el mismo rango aproximado (51.222.169.X). Si el administrador de DNS
