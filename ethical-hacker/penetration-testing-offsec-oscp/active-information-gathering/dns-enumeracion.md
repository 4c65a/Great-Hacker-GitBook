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
