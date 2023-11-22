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

# Adquisición de cuenta (Account Takeover)

La mecánica subyacente y el motivo del atacante de un ataque de apropiación de cuentas en la nube son los mismos que para una apropiación de cuentas que se lleva a cabo en las instalaciones. En una apropiación de cuentas , el actor de amenazas obtiene acceso a una cuenta de usuario o aplicación y la utiliza para luego obtener acceso a más cuentas e información. Hay diferentes formas en que puede ocurrir una apropiación de cuenta en la nube.&#x20;

Algunas de las mayores diferencias son la capacidad de la organización para detectar una apropiación de una cuenta en la nube, descubrir qué se vio afectado y determinar cómo remediarlo y recuperarlo.

Hay varias formas de detectar ataques de apropiación de cuentas.

**Ubicación de inicio de sesión**

La ubicación del usuario puede indicarle una adquisición. Por ejemplo, no puede hacer negocios en determinadas ubicaciones geográficas y países. Puede evitar que un usuario inicie sesión desde direcciones IP que residen en esas ubicaciones. Sin embargo, tenga en cuenta que un atacante puede utilizar fácilmente una VPN para evitar esta restricción.

**Intentos fallidos de inicio de sesión**

Ahora es bastante fácil detectar y bloquear intentos fallidos de inicio de sesión de un usuario o atacante.\
**Correos electrónicos de phishing laterales**

Se trata de correos electrónicos de phishing que se originan en una cuenta que ya ha sido comprometida por el atacante.

**Conexiones maliciosas de OAuth, SAML u OpenID Connect**

Un atacante podría crear una aplicación falsa que podría requerir permisos de lectura, escritura y envío para ofertas de correo electrónico SaaS como Office 365 y Gmail. Una vez que el usuario concede permiso a la aplicación para "conectarse" y autenticarse en estos servicios, el atacante podría manipularla.

**Compartir y descargar archivos anormales**

Podría sospechar de un ataque de apropiación de cuenta si nota que un usuario en particular comparte o descarga repentinamente una gran cantidad de archivos.

<mark style="color:red;">**Recursos**</mark>

{% embed url="https://www.cloudflare.com/en-gb/learning/access-management/account-takeover/" %}
