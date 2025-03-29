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

# Ataques de gemelos malvados

En un ataque gemelo malvado , el atacante crea un punto de acceso no autorizado y lo configura exactamente igual que la red corporativa existente.

Normalmente, el atacante utiliza la suplantación de DNS para redirigir a la víctima a un portal cautivo clonado o a un sitio web. Cuando los usuarios inician sesión en el gemelo malvado, un pirata informático puede inyectar fácilmente un registro DNS falso en la caché de DNS, cambiando el registro DNS de todos los usuarios de la red falsa. Cualquier usuario que inicie sesión en el gemelo malvado será redirigido por el registro DNS falsificado inyectado en el caché. Un atacante que realiza un ataque de envenenamiento de la caché de DNS quiere que la caché de DNS acepta un registro falsificado. Algunas formas de defenderse contra la suplantación de DNS son el uso de filtrado de paquetes, protocolos criptográficos y funciones de detección de suplantación de identidad proporcionadas por las implementaciones inalámbricas modernas.

_Los portales cautivos_ son portales web que normalmente se utilizan en redes inalámbricas en lugares públicos como aeropuertos y cafeterías. Por lo general, se utilizan para autenticar a los usuarios o simplemente para mostrar los términos y condiciones que se aplican a los usuarios cuando utilizan la red inalámbrica. El usuario puede simplemente hacer clic en Aceptar para aceptar los términos y condiciones. En algunos casos, se solicita al usuario que vea un anuncio, proporcione una dirección de correo electrónico o realice alguna otra acción requerida. Los atacantes pueden hacerse pasar por portales cautivos para realizar ataques de ingeniería social o robar información confidencial de los usuarios.
