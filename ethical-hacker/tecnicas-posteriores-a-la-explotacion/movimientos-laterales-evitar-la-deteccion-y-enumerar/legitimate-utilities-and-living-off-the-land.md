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

Se pueden utilizar muchas utilidades legítimas diferentes de Windows, como PowerShell, Windows Management Instrumentation (WMI) y Sysinternals, para actividades posteriores a la explotación, como se describe en las siguientes secciones. De manera similar, puede utilizar herramientas legítimas y aplicaciones instaladas en sistemas Linux y macOS para realizar actividades posteriores a la explotación. Si un sistema comprometido tiene Python instalado, por ejemplo, puede usarlo para explotación y exfiltración adicionales. De manera similar, puede utilizar el shell Bash y herramientas como Netcat post-explotación.

El uso de herramientas legítimas para realizar actividades posteriores a la explotación a menudo se conoce como _**vivir de la tierra**_ y, en algunos casos, como _**malware sin archivos**_ . El término _malware sin archivos_ se refiere a la idea de que no es necesario instalar ningún software o archivos binarios adicionales en el sistema comprometido. Entre los ejemplos de técnicas posteriores a la explotación para vivir de la tierra se incluyen los siguientes:

* PowerShell para tareas posteriores a la explotación
* PowerSploit e Imperio
* Sabueso
* Instrumental de administración de Windows para tareas posteriores a la explotación
* Sysinternals y PsExec
* Administración remota de Windows (WinRM) para tareas posteriores a la explotación

**PowerShell para tareas posteriores a la explotación**

Puede usar PowerShell para obtener listados de directorios, copiar y mover archivos, obtener una lista de procesos en ejecución y realizar tareas administrativas. La Tabla 8-4 enumera y describe algunos de los comandos de PowerShell más útiles que se pueden utilizar para tareas posteriores a la explotación.

_**Tabla 8- 4**_ _- Comandos útiles de PowerShell para tareas posteriores a la explotación_
