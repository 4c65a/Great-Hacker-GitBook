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

# Nikto

**Parte 1: Inicie Nikto y realice un escaneo básico**

* **Comando para iniciar Nikto:** `nikto --help`
* **Pregunta:** ¿Qué opción de comando descubrirá únicamente vulnerabilidades de inyección SQL?

**Parte 2: Utilice Nikto para escanear varios servidores web**

* **Comando para escanear el servidor** [**http://scanme.nmap.org**](http://scanme.nmap.org/)**:** `nikto -h scanme.nmap.org`
* **Pregunta:** ¿Qué limitaciones sugiere Nmap.org para el uso de su servidor?

**Parte 3: Investigar las vulnerabilidades del sitio web**

* **Comando para escanear varias direcciones IP desde un archivo:** `nikto -h IP_list.txt`
* **Pregunta:** ¿Cuántos de los objetivos alojan servidores web? ¿Cuántos servidores ejecutan Apache?
* **Pregunta:** ¿Qué vulnerabilidades describen los dos CVE enumerados para el servidor web 172.17.0.2?
* **Pregunta:** ¿Cuál es la solución proporcionada para CVE-2003-1418?

**Parte 4: Exportar resultados de Nikto a un archivo**

* **Comando para exportar resultados a un archivo HTML:** `nikto -h 172.17.0.2 -o scan_results.htm`
* **Comando para exportar resultados a un archivo de texto CSV:** `nikto -h 172.17.0.2 -o scan_results.txt -Formato csv`
* **Pregunta:** ¿En qué se diferencia el archivo guardado del resultado que se muestra en la pantalla?

**Reflexión**
