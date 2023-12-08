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

Algunos de estos sitios difuminan la línea entre la recopilación pasiva y activa de información, pero el punto clave para nuestros propósitos es que un tercero inicia cualquier escaneo o verificación.

Uno de esos sitios, Security Headers, analizará los encabezados de respuesta HTTP y proporcionará un análisis básico de la postura de seguridad del sitio objetivo. Podemos usar esto para tener una idea de las prácticas de codificación y seguridad de una organización en función de los resultados.

El endurecimiento del servidor es el proceso general de asegurar un servidor mediante la configuración. Esto incluye procesos como deshabilitar servicios innecesarios, eliminar servicios o cuentas de usuario no utilizados, rotar contraseñas predeterminadas, configurar encabezados de servidor apropiados.

Otra herramienta de escaneo que podemos usar es SSL Server Test de Qualys SSL Labs. Esta herramienta analiza la configuración de SSL/TLS de un servidor y la compara con las mejores prácticas actuales. También identificará algunas vulnerabilidades relacionadas con SSL/TLS, como Poodle o Heartbleed.

La desactivación de la suite TLS\_DHE\_RSA\_WITH\_AES\_256\_CBC\_SHA se ha recomendado durante varios años,debido a múltiples vulnerabilidades tanto en el modo de encadenamiento de bloques de cifrado AES como en el algoritmo SHA1. Podemos utilizar estos hallazgos para obtener información sobre las prácticas de seguridad, o la falta de ellas, dentro de la organización objetivo.

\
