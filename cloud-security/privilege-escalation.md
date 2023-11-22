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

# Privilege Escalation

_**La escalada de privilegios**_ es el acto de explotar un error o una falla de diseño en una aplicación de software o firmware para obtener acceso a recursos que normalmente habrían estado protegidos de una aplicación o un usuario. Esto da como resultado que un usuario obtenga privilegios adicionales más allá de los que el desarrollador de la aplicación pretendía originalmente (por ejemplo, un usuario normal obtiene control administrativo o un usuario en particular puede leer el correo electrónico de otro usuario sin autorización).

El desarrollador original no tiene la intención de que el atacante obtenga niveles más altos de acceso, pero probablemente no aplica adecuadamente una política de necesidad de conocimiento y/o no ha validado el código de la aplicación adecuadamente. Los atacantes aprovechan esto para acceder a áreas protegidas de los sistemas operativos o a las aplicaciones (por ejemplo, leyendo el correo electrónico de otro usuario sin autorización). Los desbordamientos de búfer también se utilizan en computadoras con Windows para elevar los privilegios. Para eludir la gestión de derechos digitales (DRM) en juegos y música, los atacantes utilizan un método conocido como _jailbreaking_ , que es otro tipo de escalada de privilegios, que se encuentra más comúnmente en dispositivos móviles basados ​​en Apple iOS. El malware también intenta explotar las vulnerabilidades de escalada de privilegios, si existe alguna en el sistema. También se puede intentar escalar privilegios en dispositivos de red. Generalmente, la solución para esto es simplemente actualizar el dispositivo y buscar actualizaciones periódicamente.

Los siguientes son un par de tipos diferentes de escalada de privilegios:

**Escalada de privilegios verticales**

Este tipo de escalada de privilegios, también llamada elevación de privilegios, ocurre cuando un usuario con privilegios bajos accede a funciones reservadas para usuarios con privilegios mayores (por ejemplo, un usuario estándar que accede a funciones de un administrador). Para protegerse contra esta situación, debe actualizar el firmware del dispositivo de red. En el caso de un sistema operativo, conviene actualizarlo nuevamente. También es recomendable el uso de algún tipo de sistema de control de acceso, por ejemplo, Control de cuentas de usuario (UAC).

**Escalada de privilegios horizontales**

Este tipo de escalada de privilegios ocurre cuando un usuario normal accede a funciones o contenido reservado para otros usuarios normales (por ejemplo, un usuario lee el correo electrónico de otro). Esto se puede hacer mediante piratería informática o mediante una persona que se acerca a la computadora de otra persona y simplemente lee su correo electrónico. Haga que sus usuarios siempre bloqueen su computadora (o cierren sesión) cuando no estén físicamente en su escritorio.
