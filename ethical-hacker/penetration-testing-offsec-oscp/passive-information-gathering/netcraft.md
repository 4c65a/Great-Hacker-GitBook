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

# Netcraft

**Netcraft :** Una herramienta para la recopilación pasiva de información

Estas funciones incluyen la detección de tecnologías utilizadas en un sitio web específico y la identificación de otros hosts que comparten el mismo bloque de red IP.

Utilizar servicios como Netcraft se considera una técnica pasiva de reconocimiento, ya que no interactuamos directamente con nuestro objetivo.

**Analicemos algunas de las capacidades de Netcraft:**

* **Búsqueda de DNS:** Podemos utilizar la página de búsqueda de DNS de Netcraft&#x20;
* **Informes de sitios:** Para cada servidor encontrado, podemos ver un "informe de sitio" que proporciona información adicional e histórica sobre el servidor haciendo clic en el ícono de archivo junto a la URL de cada sitio.

El inicio del informe cubre la información de registro del dominio.

* **Servidor web:** El software que ejecuta el sitio web (por ejemplo, Apache, Nginx).
* **Sistema operativo:** El sistema operativo del servidor (por ejemplo, Linux, Windows).
* **Lenguajes de programación:** Los lenguajes de programación utilizados para desarrollar el sitio web (por ejemplo, PHP, Python).
* **Bases de datos:** El software de base de datos utilizado para almacenar la información del sitio web (por ejemplo, MySQL, PostgreSQL).
* **Certificados SSL:** La presencia y detalles de los certificados de seguridad SSL utilizados para cifrar el tráfico del sitio web.

Esta información puede ser invaluable para la fase de reconocimiento de una prueba de penetración, ya que nos permite comprender la infraestructura tecnológica del objetivo y, en consecuencia, identificar posibles vulnerabilidades.
