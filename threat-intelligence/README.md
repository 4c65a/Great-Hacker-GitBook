---
icon: masks-theater
---

# Threat Intelligence

#### Convenciones de nomenclatura de actores de amenazas

En ciberseguridad, diferentes empresas utilizan distintas convenciones para nombrar y clasificar a los grupos maliciosos, lo que puede generar confusión al comparar informes o análisis. Además, muchos actores comparten herramientas o técnicas, dificultando su atribución precisa.

Las dos convenciones más reconocidas y utilizadas son las de **CrowdStrike** y **FireEye/Mandiant**.

***

**CrowdStrike**

CrowdStrike clasifica a los grupos principalmente según su país de origen o motivación, empleando nombres de animales para los actores estatales y nombres simbólicos relacionados con la intención para grupos no estatales.

* **Actores estatales (nombres de animales):**

| Animal   | País            | Ejemplo           |
| -------- | --------------- | ----------------- |
| Oso      | Rusia           | Fancy Bear        |
| Búfalo   | Vietnam         | —                 |
| Chollima | Corea del Norte | Stardust Chollima |
| Grulla   | Corea del Sur   | —                 |
| Gatito   | Irán            | Gatito Refinado   |
| Leopardo | Pakistán        | Leopardo Mítico   |
| Panda    | China           | Panda Duende      |
| Tigre    | India           | Virrey Tigre      |

* **Actores no estatales (según motivación):**

| Nombre | Tipo de grupo                    | Ejemplo               |
| ------ | -------------------------------- | --------------------- |
| Chacal | Grupos activistas (hacktivistas) | —                     |
| Spider | Grupos criminales                | Mummy Spider (Emotet) |

***

**FireEye / Mandiant**

Esta convención utiliza un sistema numérico con prefijos para diferenciar los tipos de actores:

* **APT** (Advanced Persistent Threat): grupos generalmente estatales o patrocinados por gobiernos.
* **FIN**: grupos criminales financieros.
* **APT por país:**

| País            | Grupos APT                                                 |
| --------------- | ---------------------------------------------------------- |
| China           | APT1, APT2, APT3, APT10, APT19, APT20, APT30, APT40, APT41 |
| Irán            | APT33, APT34, APT35, APT39                                 |
| Corea del Norte | APT37, APT38                                               |
| Rusia           | APT28, APT29                                               |
| Vietnam         | APT32                                                      |

* **Grupos financieros (FIN):**

FIN4, FIN5, FIN6, FIN7, FIN8, FIN10

* **Grupos no clasificados:**

UNC (Unclassified): actores sin clasificación clara o atribución definida.

***

Este sistema ayuda a la comunidad a identificar y referenciar actores de amenazas de manera estandarizada, facilitando la colaboración y el análisis compartido.

### Ejemplos de investigación de actores de amenazas y herramientas recomendadas

Investigar un actor de amenaza implica recolectar, analizar y correlacionar información técnica y contextual para entender su modus operandi, infraestructura y objetivos. Aquí te dejo pasos prácticos y las herramientas que facilitan cada etapa.

***

#### 1. Identificación inicial y reconocimiento

**Objetivo:** Encontrar referencias al actor, campañas conocidas, herramientas usadas y tácticas reportadas.

* **Cómo hacerlo:**
  * Buscar reportes públicos de empresas de ciberseguridad (CrowdStrike, FireEye, Mandiant, Recorded Future, etc.).
  * Analizar IOC (Indicators of Compromise) asociados a un actor (IPs, dominios, hashes, firmas).
  * Consultar bases de datos de amenazas y feeds públicos.
* **Herramientas:**
  * **VirusTotal:** Analiza archivos, URLs y extrae indicadores asociados.
  * **AlienVault OTX:** Plataforma colaborativa con IOC y reportes.
  * **MISP (Malware Information Sharing Platform):** Plataforma para compartir IOC y atributos de actores.
  * **ThreatFox (Abuse.ch):** IOC públicos relacionados con amenazas conocidas.

***

#### 2. Análisis técnico de malware y herramientas

**Objetivo:** Analizar muestras de malware o herramientas usadas por el actor para descubrir técnicas y funcionalidades.

* **Cómo hacerlo:**
  * Análisis estático: examinar el binario sin ejecutarlo para extraer información (hashes, strings, imports).
  * Análisis dinámico: ejecutar en un entorno controlado (sandbox) para observar comportamiento.
* **Herramientas:**
  * **IDA Pro / Ghidra:** Desensambladores para análisis estático profundo.
  * **Cuckoo Sandbox:** Sandbox automatizado para análisis dinámico.
  * **PEStudio:** Análisis estático de ejecutables Windows.
  * **Process Monitor (Sysinternals):** Monitorea actividad en tiempo real.
  * **YARA:** Regla para detectar patrones de malware.

***

#### 3. Análisis de infraestructura y TTP (Tactics, Techniques and Procedures)

**Objetivo:** Mapear infraestructura C2 (comando y control), dominios, IPs, y entender técnicas usadas (phishing, spear phishing, exploits).

* **Cómo hacerlo:**
  * Analizar tráfico de red.
  * Investigar dominios y certificados SSL.
  * Buscar patrones de comportamiento en campañas.
* **Herramientas:**
  * **Wireshark:** Captura y análisis de tráfico de red.
  * **PassiveTotal (RiskIQ):** Investigación de infraestructura y dominios.
  * **Shodan:** Buscar dispositivos conectados y servicios.
  * **Censys:** Información sobre certificados y hosts.
  * **SpiderFoot:** OSINT automatizado para recopilar información sobre dominios, IPs y actores.

***

#### 4. Correlación y reporte

**Objetivo:** Documentar hallazgos, relacionar IOC y elaborar informes para tomar decisiones de defensa.

* **Cómo hacerlo:**
  * Agrupar IOC por actor o campaña.
  * Crear reportes claros y con recomendaciones.
* **Herramientas:**
  * **MISP:** Para almacenar y compartir IOC.
  * **ELK Stack (Elasticsearch, Logstash, Kibana):** Para análisis y visualización de datos.
  * **TheHive:** Plataforma para gestión de incidentes y análisis colaborativo.

***

#### Resumen rápido de herramientas clave

| Etapa                 | Herramientas principales                            |
| --------------------- | --------------------------------------------------- |
| Reconocimiento        | VirusTotal, AlienVault OTX, MISP, ThreatFox         |
| Análisis técnico      | IDA Pro, Ghidra, Cuckoo Sandbox, PEStudio, YARA     |
| Infraestructura y TTP | Wireshark, PassiveTotal, Shodan, Censys, SpiderFoot |
| Correlación y reporte | MISP, ELK Stack, TheHive                            |

