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

# DNS Cache Poisoning

Es otro ataque popular aprovechado por los actores de amenazas.

DNS Cache Poisoning implica la manipulación de la caché de resolución de DNS mediante la inyección de datos de DNS corruptos. Esto se hace para obligar al servidor DNS a enviar la dirección IP incorrecta a la víctima y redirigir a la víctima al sistema del atacante.&#x20;

**En proceso**

### Mitigar&#x20;

**Dependencia Mínima de Relaciones de Confianza:** Configurar los servidores DNS de manera que minimicen la dependencia de relaciones de confianza con otros servidores DNS, reduciendo así la superficie de ataque.

**Características de BIND 9.5.0 y Posteriores:** Utilizar versiones de BIND (Berkeley Internet Name Domain) 9.5.0 y superiores, que ofrecen funciones como la aleatorización de puertos y el suministro de identificadores de transacciones DNS criptográficamente seguros para prevenir ataques de envenenamiento de la caché de DNS.

**Limitar Consultas Recursivas:** Restringir las consultas DNS recursivas para reducir la exposición al riesgo. Limitar el acceso solo a aquellos sistemas confiables y necesarios.

**Almacenar sólo Datos Relevantes:** Configurar los servidores DNS para almacenar únicamente datos relacionados con el dominio solicitado, minimizando así la información susceptible a envenenamiento.

**Restringir Respuestas a Consultas:** Limitar las respuestas a las consultas DNS para proporcionar información solo sobre el dominio solicitado, evitando revelar detalles innecesarios que podrían ser utilizados en ataques.

**DNSSEC (Extensiones de Seguridad del DNS):** Implementar DNSSEC, una tecnología desarrollada por el IETF, que ofrece autenticación segura de datos DNS. Esto proporciona una capa adicional de protección contra ataques de envenenamiento de la caché de DNS al garantizar la integridad y autenticidad de los datos DNS.
