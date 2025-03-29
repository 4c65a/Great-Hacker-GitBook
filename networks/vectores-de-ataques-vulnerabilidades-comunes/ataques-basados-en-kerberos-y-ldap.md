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

# Ataques basados ​​en Kerberos y LDAP

Kerberos es un protocolo de autenticación definido en RFC 4120 que Windows ha utilizado durante varios años.Es un protocolo que facilita la autenticación mutua a través de una red que no es de confianza y la autorización de un cliente  a servicios.

Una implementación de Kerberos contiene tres elementos básicos:

* Cliente
* Servidor
* Centro de distribución de claves (KDC), incluido el servidor de autenticación y el servidor de concesión de tickets

### _Pasos de la autenticación Kerberos_

**Paso 1** . El cliente envía una solicitud al servidor de autenticación dentro del KDC.

**Paso 2** . El servidor de autenticación envía una clave de sesión y un ticket de concesión de tickets (TGT) que se utiliza para verificar la identidad del cliente.

**Paso 3** . El cliente envía el TGT al servidor de concesión de tickets.

**Paso 4** . El servidor que otorga tickets genera y envía un ticket al cliente.

**Paso 5** . El cliente presenta el ticket al servidor.

**Paso 6** . El servidor otorga acceso al cliente.

Active Directory utiliza el Protocolo ligero de acceso a directorios (LDAP) como protocolo de acceso. La implementación de LDAP de Windows admite la autenticación Kerberos. LDAP utiliza una estructura jerárquica de árbol invertido llamada árbol de información de directorio (DIT). En LDAP, cada entrada tiene una posición definida. El nombre distinguido (DN) representa la ruta completa de la entrada.

Uno de los ataques más comunes es el ataque del golden ticket de Kerberos. Un atacante puede manipular tickets de Kerberos en función de los hashes disponibles comprometiendo un sistema vulnerable y obteniendo las credenciales de usuario local y los hashes de contraseña. Si el sistema está conectado a un dominio, el atacante puede identificar un hash de contraseña Kerberos TGT (KRBTGT) para obtener el ticket dorado.



Empire es una herramienta popular que se puede utilizar para realizar golden ticket y muchos otros tipos de ataques. Empire es básicamente un marco de trabajo posterior a la explotación que incluye un agente de Windows PowerShell puro y un agente de Python.&#x20;

Con Empire, puede ejecutar agentes PowerShell sin necesidad de utilizar powershell.exe.

```bash
(Empire) > use module powershell/credentials/mimikatz/golden_ticket
```

Un ataque similar es el _ataque del ticket plateado Kerberos_ . _Los boletos plateados_ son boletos de servicio falsificados para un servicio determinado en un servidor en particular. El sistema de archivos común de Internet (CIFS) de Windows le permite acceder a archivos en un servidor en particular, y el servicio HOST le permite ejecutar **schtasks.exe** o Instrumental de administración de Windows (WMI) en un servidor determinado. Para crear un ticket plateado, necesita la cuenta del sistema (que termina en $), el identificador de seguridad (SID) del dominio, el nombre de dominio completo y el servicio proporcionado (por ejemplo, CIFS, HOST).

Otra debilidad en las implementaciones de Kerberos es el uso de la delegación Kerberos sin restricciones. La delegación de Kerberos es una característica que permite que una aplicación reutilice las credenciales del usuario final para acceder a recursos alojados en un servidor diferente. Normalmente, debería permitir la delegación de Kerberos sólo si, en última instancia, se confía en el servidor de aplicaciones; sin embargo, permitirlo podría tener consecuencias de seguridad negativas si se abusa y, por lo tanto, la delegación de Kerberos no está habilitada de forma predeterminada en Active Directory.

### Kerberoasting

Es una actividad posterior a la explotación que utiliza un atacante para extraer hashes de credenciales de cuentas de servicio de Active Directory para descifrarlos sin conexión. Es un ataque generalizado que aprovecha una combinación de implementaciones de cifrado débiles y prácticas de contraseñas inadecuadas,puede ser un ataque eficaz porque el actor de la amenaza puede extraer hashes de credenciales de cuentas de servicio sin enviar ningún paquete IP a la víctima y sin tener credenciales de administrador de dominio.
