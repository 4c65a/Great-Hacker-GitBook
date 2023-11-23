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

# Escaneo post-explotación

El movimiento lateral implica escanear una red en busca de otros sistemas, explotar vulnerabilidades en otros sistemas, comprometer credenciales y recopilar información confidencial para su filtración. El movimiento lateral es posible si una organización no segmenta su red adecuadamente.,la segmentación de la red es muy importante.

Es muy importante probar la efectividad de su estrategia de segmentación de red. Es posible que su organización haya implementado firewalls virtuales o físicos, redes de área local virtuales (VLAN) o políticas de control de acceso para la segmentación, o podría utilizar microsegmentación en entornos virtualizados y en contenedores.

Después de comprometer un sistema, puede utilizar escaneos de puertos básicos para identificar sistemas o servicios de interés que puede atacar aún más en un intento de comprometer información valiosa.

Un atacante debe evitar generar alarmas en esta etapa. Si los defensores de la seguridad detectan que hay una amenaza en la red, la examinarán minuciosamente y frustrarán cualquier progreso que haya logrado. En algunos casos de pruebas de penetración, puede comenzar de manera muy sigilosa y aumentar gradualmente la cantidad de tráfico y herramientas automatizadas utilizadas para probar también la efectividad de los defensores de la seguridad (incluido el centro de operaciones de seguridad \[SOC]).

Puede buscar recursos compartidos SMB en los que pueda iniciar sesión con credenciales comprometidas o a los que el usuario que inició sesión en el sistema comprometido pueda tener acceso. Puede mover archivos hacia o desde otros sistemas. Alternativamente, puede crear una instancia de un recurso compartido SMB y copiar archivos desde un sistema comprometido.

Puede utilizar protocolos de acceso remoto, incluidos los siguientes, para comunicarse con un sistema comprometido:

* Protocolo de escritorio remoto (RDP) de Microsoft
* Escritorio remoto de Apple
* VNC
* reenvío del servidor X

Este módulo de Metasploit habilita RDP y proporciona opciones para crear una cuenta y configurarla para que sea miembro del grupo de administradores locales y usuarios de escritorio remoto. Este módulo también se puede utilizar para reenviar el puerto TCP 3389 del objetivo.

### _Uso del módulo de post explotación RDP de Metasploit_

```
msf > use post/windows/manage/enable_rdp
msf post(windows/manage/enable_rdp) > show options
Module options (post/windows/manage/enable_rdp):
   Name    Current Setting Required Description
   ----    --------------- -------- -----------
   ENABLE  true              no       Enable the RDP Service and
                                        Firewall Exception.
   FORWARD false            no       Forward remote port 3389 to local
                                        Port.
   LPORT    3389             no       Local port to forward remote
                                        connection.
   PASSWORD                  no       Password for the user created.
   SESSION                   yes      The session to run this module
                                        on.
  USERNAME                   no       The username of the user to
                                        create.
 meterpreter > run
```
