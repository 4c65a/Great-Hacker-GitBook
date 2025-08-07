---
icon: asterisk
---

# Digital Forensics

### ¿Qué es la investigación forense digital?

Es la **rama especializada** de la ciencia forense enfocada en recolectar, preservar, analizar y presentar evidencia digital con validez legal.

Objetivos principales:

* Asegurar **autenticidad** e **integridad** de las pruebas.
* Permitir su **admisibilidad ante un tribunal**.
* Resolver delitos como:
  * Cibercrimen.
  * Robo de propiedad intelectual.
  * Fraude.
  * Amenazas internas.

#### Aplicación en ciberseguridad:

Se vincula a:

* Monitoreo de empleados.
* Respuesta a incidentes.
* Investigación de ataques (DFIR: _Digital Forensics and Incident Response_).

***

### Tipos de análisis forense digital

| Tipo                                | Descripción                                          |
| ----------------------------------- | ---------------------------------------------------- |
| **Informática forense**             | Pruebas extraídas de computadoras, discos y medios.  |
| **Forense de redes**                | Análisis de tráfico, conexiones, IPs, sitios web.    |
| **Forense de memoria (RAM)**        | Recupera datos de la memoria viva.                   |
| **Forense de dispositivos móviles** | Pruebas desde celulares, tablets, tarjetas SIM, etc. |

***

### Beneficios clave

1. **Soporte a la respuesta ante incidentes**
   * Preserva evidencia crítica.
   * Ayuda a detectar malware, intrusiones y amenazas internas.
2. **Validez legal y cadena de custodia**
   * Pruebas deben estar seguras, sin alteraciones.
   * Base para el procesamiento judicial.
3. **Monitoreo de empleados sospechosos**
   * Identificación de navegación indebida, descarga de archivos prohibidos o fuga de datos.
   * Pruebas útiles para Recursos Humanos o autoridades.

***

### Roles asociados en un SOC

| Rol                                     | Función relacionada con forense                                                        |
| --------------------------------------- | -------------------------------------------------------------------------------------- |
| **Analista SOC Nivel 1 (T1)**           | Investigación inicial, recopila IPs, dominios, emails como evidencia.                  |
| **Analista SOC Nivel 2/3 (T2/T3)**      | Casos críticos. Requiere manejo riguroso de evidencia.                                 |
| **Analista de malware**                 | Analiza muestras para entender su funcionamiento e IOCs.                               |
| **Analista forense digital**            | Casos escalados, monitoreo de empleados, colaboración con SIRT.                        |
| **Analista de amenazas internas**       | Enfocado en detectar y documentar conductas sospechosas dentro de la empresa.          |
| **Cazador de amenazas (Threat Hunter)** | Busca indicadores de ataques avanzados; requiere conocimientos forenses.               |
| **Respondedor de incidentes**           | Amplio rango de habilidades; trabaja con examinadores forenses para análisis profundo. |

***

### Herramientas del oficio — Forense Digital

#### Recopilación de pruebas (Imágenes, artefactos, datos crudos)

| Herramienta    | Descripción rápida                                                                                                    | Comando básico de uso (CLI o GUI)                                                                                             |
| -------------- | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **KAPE**       | Automatiza la recolección de artefactos (navegador, logs, programas ejecutados, etc.). Muy usada en entornos Windows. | `kape.exe --target TargetList --module ModuleList --vhdx MyImage.vhdx` _(requiere configuración previa de targets y módulos)_ |
| **FTK Imager** | Crea imágenes forenses de discos o RAM. Permite navegar por imágenes como si fueran reales.                           | Solo GUI: abre la herramienta y selecciona **"Create Disk Image"**. También puede exportar evidencia.                         |
| **EnCase**     | Suite avanzada comercial. Captura imágenes forenses de PCs, móviles e IoT.                                            | GUI propietaria. Inicia desde **"New Case" > "Acquire Evidence"**.                                                            |
| **Cellebrite** | Herramienta líder en adquisición de datos de móviles. Extrae mensajes, apps, ubicaciones.                             | GUI. Comienza con **UFED Physical Analyzer** > conecta el dispositivo móvil > **"Extract Data"**.                             |

***

#### Análisis de evidencia (Datos procesados e indexados)

| Herramienta    | Descripción rápida                                                                                  | Comando básico de uso                                                                                                                                                                    |
| -------------- | --------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Autopsy**    | Herramienta gráfica open source. Extrae programas usados, archivos eliminados, navegación web, etc. | GUI. Comienza nuevo caso desde **"Create New Case"** > añade imagen > **"Ingest Modules"**.                                                                                              |
| **Volatility** | Analiza volcados de memoria RAM. Extrae procesos, conexiones, DLLs, etc.                            | <p>Ejemplo básico:<br><code>vol.py -f memory.dmp --profile=Win10x64_19041 pslist</code><br><em>(Requiere definir perfil del SO y tipo de análisis: pslist, dlllist, netscan...)</em></p> |

***

### Tips útiles para SOC o DFIR:

* **KAPE**: útil en la primera fase de respuesta rápida, mientras se realiza el volcado completo.
* **FTK Imager** o **EnCase**: ideales para mantener la cadena de custodia, ya que permiten hashes y logs confiables.
* **Autopsy**: excelente para analistas de SOC que necesitan revisar múltiples evidencias rápidamente sin línea de comandos.
* **Volatility**: esencial si estás investigando malware en ejecución o rootkits.

