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

# Security Headers and SSL/TLS

### Recopilación de información pasiva de la postura de seguridad de un sitio web

**Existen varios sitios web especializados que podemos utilizar para recopilar información sobre la postura de seguridad de un sitio web o dominio.** Algunos de estos sitios difuminan la línea entre la recopilación pasiva y activa de información, pero el punto clave para nuestros propósitos es que un tercero inicia cualquier escaneo o verificación.

**Uno de esos sitios, Security Headers, analizará los encabezados de respuesta HTTP y proporcionará un análisis básico de la postura de seguridad del sitio objetivo.** Podemos usar esto para tener una idea de las prácticas de codificación y seguridad de una organización en función de los resultados.

**El sitio carece de varios encabezados defensivos, como Content-Security-Policy y X-Frame-Options.** Estos encabezados faltantes no son necesariamente vulnerabilidades en sí mismos, pero podrían indicar que los desarrolladores web o los administradores de servidores no están familiarizados con el endurecimiento de servidores.

**El endurecimiento del servidor es el proceso general de asegurar un servidor mediante la configuración.** Esto incluye procesos como deshabilitar servicios innecesarios, eliminar servicios o cuentas de usuario no utilizados, rotar contraseñas predeterminadas, configurar encabezados de servidor apropiados, etc. No necesitamos conocer todos los detalles de la configuración de cada tipo de servidor, pero comprender los conceptos y qué buscar puede ayudarnos a determinar la mejor manera de abordar un objetivo potencial.

**Otra herramienta de escaneo que podemos usar es SSL Server Test de Qualys SSL Labs.** Esta herramienta analiza la configuración de SSL/TLS de un servidor y la compara con las mejores prácticas actuales. También identificará algunas vulnerabilidades relacionadas con SSL/TLS, como Poodle o Heartbleed.

**Los resultados parecen mejores que la verificación de Security Headers. Sin embargo, esto muestra que el servidor admite versiones TLS como 1.0 y 1.1, que se consideran heredadas ya que implementan conjuntos de cifrado inseguros.** En última instancia, esto sugiere que nuestro objetivo no está aplicando las mejores prácticas actuales para el endurecimiento de SSL/TLS.

**La desactivación de la suite TLS\_DHE\_RSA\_WITH\_AES\_256\_CBC\_SHA se ha recomendado durante varios años, por ejemplo, debido a múltiples vulnerabilidades tanto en el modo de encadenamiento de bloques de cifrado AES como en el algoritmo SHA1.** Podemos utilizar estos hallazgos para obtener información sobre las prácticas de seguridad, o la falta de ellas, dentro de la organización objetivo.

**En resumen:**

* Podemos utilizar sitios web especializados para recopilar información pasiva sobre la postura de seguridad de un sitio web o dominio.
* Estos sitios analizan factores como los encabezados de respuesta HTTP y la configuración de SSL/TLS.
* Los resultados de estas herramientas pueden ayudarnos a tener una idea de las prácticas de seguridad de una organización.
* Podemos utilizar esta información para planificar y realizar nuestra prueba de penetración de manera más efectiva.

\
