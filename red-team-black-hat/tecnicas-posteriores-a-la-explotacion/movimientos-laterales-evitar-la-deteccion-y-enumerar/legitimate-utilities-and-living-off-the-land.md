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

# Legitimate Utilities and Living-off-the-Land

Se pueden utilizar muchas utilidades legítimas diferentes de Windows, como PowerShell, Windows Management Instrumentation (WMI) y Sysinternals, para actividades posteriores a la explotación, como se describe en las siguientes secciones. De manera similar, puede utilizar herramientas legítimas y aplicaciones instaladas en sistemas Linux y macOS para realizar actividades posteriores a la explotación. Si un sistema comprometido tiene Python instalado, puede usarlo para explotación y exfiltración adicionales. De manera similar, puede utilizar el shell Bash y herramientas como Netcat post-explotación.

El uso de herramientas legítimas para realizar actividades posteriores a la explotación a menudo se conoce como vivir de la tierra (Living off the Land) y, en algunos casos, como malware sin archivos (Fileless Malware). El término _malware sin archivos_ se refiere a la idea de que no es necesario instalar ningún software o archivos binarios adicionales en el sistema comprometido. Entre los ejemplos de técnicas posteriores a la explotación para vivir de la tierra se incluyen los siguientes:

* **PowerShell for Post-Exploitation Tasks**
* **PowerSploit and Empire**
* **BloodHound**
* **Windows Management Instrumentation for Post-Exploitation Tasks**
* **Sysinternals and PsExec**
* **Windows Remote Management (WinRM) for Post-Exploitation Tasks**

**PowerShell para tareas posteriores a la explotación**

PowerShell para obtener listados de directorios, copiar y mover archivos, obtener una lista de procesos en ejecución y realizar tareas administrativas.

**PowerSploit y Empire**

PowerSploit es una colección de módulos de PowerShell que se pueden utilizar para la post-explotación y otras fases de una evaluación.&#x20;

Cuando utiliza PowerSploit, normalmente expone los scripts que inician un servicio web.Se inicia un servicio web simple usando el comando **sudo python3 -m http.server 1337**. Luego, el sistema comprometido se conecta a la máquina del atacante en el puerto 1337 y descarga un script PowerSploit para la filtración de datos.

Otro marco de post-explotación basado en PowerShell es Empire , que es un marco de código abierto que incluye un agente PowerShell para Windows y un agente Python para Linux. Empire implementa la capacidad de ejecutar agentes PowerShell sin la necesidad de powershell.exe. Le permite implementar rápidamente módulos posteriores a la explotación, incluidos registradores de teclas, shells de enlace , shells inversos , Mimikatz y comunicaciones adaptables para evadir la detección.

Módulos de Empire una instantánea de la cámara web de macOS X. Este módulo toma una fotografía utilizando la cámara web de un sistema macOS X comprometido.

**La herramienta pos-explotación del Imperio.**

```
(Empire) > usemodule python/collection/osx/webcam
(Empire: python/collection/osx/webcam) > info

                        Name: Webcam
                      Module: python/collection/osx/webcam
                  NeedsAdmin: False
                   OpsecSafe: False
                    Language: python
          MinLanguageVersion: 2.6
                  Background: False
             OutputExtension: png

Authors:
   @harmj0y

Description:
   Takes a picture of a person through OSX’s webcam with an
   ImageSnap binary.

Comments:
   http://iharder.sourceforge.net/current/macosx/imagesnap/

Options:

 Name    Required  Value Description
 ----     -------- ------- -----------
 TempDir True       /tmp/   Temporary directory to drop the
                               ImageSnap binary and picture.
                               Agent True Agent to execute module on.
(Empire: python/collection/osx/webcam)>

```

**BloodHound**

Puede utilizar una aplicación web JavaScript de una sola página llamada BloodHound que utiliza la teoría de grafos para revelar las relaciones ocultas en un entorno de Windows Active Directory. Un atacante puede utilizar BloodHound para identificar numerosas rutas de ataque. De manera similar, los equipos de respuesta a incidentes pueden utilizar BloodHound para detectar y eliminar esas mismas rutas de ataque(también rutas compleja de azure).

**Windows Management Instrumentation for Post-Exploitation Tasks**

El Instrumental de administración de Windows (WMI) se utiliza para administrar datos y operaciones en sistemas operativos Windows. Puede escribir scripts o aplicaciones WMI para automatizar tareas administrativas en computadoras remotas. WMI también proporciona funcionalidad para la administración de datos a otras partes del sistema operativo, incluido System Center Operations Manager (anteriormente Microsoft Operations Manager \[MOM]) y Windows Remote Management (WinRM). El malware puede utilizar WMI para realizar diferentes actividades en un sistema comprometido. Por ejemplo, el ransomware Nyeta utilizó WMI para realizar tareas administrativas.

**Sysinternals y PsExec**

Sysinternals es un conjunto de herramientas que permite a los administradores controlar computadoras basadas en Windows desde una terminal remota. Puede utilizar Sysinternals para cargar, ejecutar e interactuar con archivos ejecutables en hosts comprometidos. Toda la suite funciona desde una interfaz de línea de comandos y se puede programar. Al utilizar Sysinternals, puede ejecutar comandos que pueden revelar información sobre procesos en ejecución y puede eliminar o detener servicios. Los probadores de penetración suelen utilizar las siguientes herramientas de Sysinternals después de la explotación:

* **PsExec:** Ejecuta procesos
* **PsFile:** Muestra archivos abiertos
* **PsGetSid:** muestra identificadores de seguridad de los usuarios.
* **PsInfo:** Proporciona información detallada sobre una computadora.
* **PsKill:** Mata procesos
* **PsList:** Muestra información sobre procesos.
* **PsLoggedOn:** enumera las cuentas registradas
* **PsLogList:** extrae registros de eventos
* **PsPassword:** Cambia contraseñas
* **PsPing:** inicia solicitudes de ping
* **PsService:** realiza cambios en los servicios de Windows
* **PsShutdown:** apaga una computadora
* **PsSuspend:** Suspende procesos

_**PsExec**_ es una de las herramientas Sysinternals más poderosas. Puede usarlo para ejecutar de forma remota cualquier cosa que pueda ejecutarse en un símbolo del sistema de Windows. También puede utilizar PsExec para modificar los valores del registro de Windows, ejecutar scripts y conectar un sistema comprometido a otro sistema. Para los atacantes, una ventaja de PsExec es que la salida de los comandos que ejecuta se muestra en su sistema en lugar de en el sistema de la víctima. Esto permite que un atacante pase desapercibido para los usuarios remotos.

**Windows Remote Management (WinRM) for Post-Exploitation Tasks**\
La administración remota de Windows (WinRM) le brinda una forma legítima de conectarse a sistemas Windows. WinRM generalmente se administra mediante la Política de grupo de Windows.

WinRM puede resultar útil para actividades posteriores a la explotación. Un atacante podría permitir que WinRM permite más conexiones a los sistemas comprometidos y mantenga el acceso persistente.
