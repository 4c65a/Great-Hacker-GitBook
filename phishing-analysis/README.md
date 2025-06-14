---
icon: fishing-rod
---

# Phishing Analysis

## Phishing: Qué es y cómo analizarlo

***

### 1. ¿Qué es el phishing?

El phishing es un ataque informático que busca engañar a la víctima para que revele información confidencial (contraseñas, datos bancarios, etc.) haciéndose pasar por una entidad confiable, generalmente a través de emails, mensajes o páginas web falsas.

Es un método efectivo porque apela al error humano, la confianza y la urgencia. Por eso, el conocimiento y el análisis riguroso son la mejor defensa.

***

### 2. Cómo identificar un email de phishing

Los correos phishing suelen tener características que los distinguen de mensajes legítimos:

* **Remitente falso o sospechoso:** La dirección no coincide con la empresa que supuestamente envía el correo.
* **Errores ortográficos o gramaticales:** Mensajes mal escritos, poco profesionales.
* **Solicitudes urgentes o amenazas:** “Tu cuenta será cerrada si no...”
* **Enlaces engañosos:** El texto del enlace parece legítimo, pero apunta a un dominio extraño o diferente.
* **Archivos adjuntos sospechosos:** Documentos con extensiones raras o ejecutables.
* **Falta de personalización:** No usan tu nombre o datos específicos.

***

### 3. Análisis práctico de un email sospechoso

#### 3.1 Inspección del encabezado (header) del correo

Los encabezados contienen información técnica que revela la ruta del email, su origen real y autenticidad.

* **Herramienta:** Puedes usar visualizadores de headers como MxToolbox Header Analyzer o hacerlo manualmente en tu cliente de correo.
* **Qué buscar:**
  * `Received:` verificar la ruta real del correo.
  * `Return-Path:` dirección real del remitente.
  * `SPF`, `DKIM` y `DMARC`: registros que indican si el correo está autorizado por el dominio real.

#### 3.2 Verificación de URLs

* **Herramientas:**
  * Hover sobre el enlace sin hacer clic para ver la URL real.
  * [VirusTotal](https://www.virustotal.com/) para analizar URLs o archivos.
  * [URLVoid](https://www.urlvoid.com/) para reputación de dominios.
* **Análisis:**
  * Comprueba que el dominio sea legítimo y no un parecido fraudulento (ejemplo: `micr0soft.com` en lugar de `microsoft.com`).
  * Verifica que la URL use HTTPS (candado en el navegador), aunque no garantiza seguridad total.

#### 3.3 Archivos adjuntos

* Analiza con antivirus actualizado.
* Puedes subir archivos sospechosos a VirusTotal para un análisis automático.

***

### 4. Análisis de páginas web sospechosas de phishing

* **Inspecciona el código fuente:** Clic derecho > Ver código fuente para detectar scripts extraños o enlaces escondidos.
* **Verifica el certificado SSL:** Haz clic en el candado para ver la información del certificado.
* **Compara la URL:** Que corresponda exactamente con la página oficial.
* **Usa sandbox o máquinas virtuales** para navegar sin riesgo.
* **Herramientas recomendadas:**
  * **PhishTank:** Base de datos colaborativa para verificar URLs sospechosas.
  * **Burp Suite:** Para analizar solicitudes, respuestas y detectar ataques.
  * **Wireshark:** Para analizar tráfico de red si sospechas de comunicación maliciosa.
  * **Cuckoo Sandbox:** Para análisis automatizado de archivos y URLs.

***

### 5. Herramientas para análisis de phishing (Email y Web)

| Herramienta               | Uso principal                            | Notas                                  |
| ------------------------- | ---------------------------------------- | -------------------------------------- |
| VirusTotal                | Escaneo de URLs, archivos y emails       | Gratuito y muy completo                |
| MxToolbox Header Analyzer | Análisis de encabezados de emails        | Rápido y sencillo                      |
| PhishTank                 | Verificar URLs sospechosas               | Comunidad colaborativa                 |
| Burp Suite                | Auditoría y análisis de aplicaciones web | Profesional, versión gratuita limitada |
| Wireshark                 | Análisis de tráfico de red               | Necesita conocimientos avanzados       |
| Cuckoo Sandbox            | Análisis automático de malware           | Requiere instalación propia            |
| URLVoid                   | Reputación de dominios                   | Complementa VirusTotal                 |

***

### 6. Buenas prácticas para evitar ser víctima

* No hagas clic en enlaces dudosos o adjuntos inesperados.
* Verifica siempre el remitente y la URL.
* Usa autenticación de dos factores (2FA).
* Mantén actualizado el sistema y antivirus.
* Educa a tu entorno sobre phishing.

***

### 7. Ejemplo básico de análisis manual de un email phishing

Supongamos que recibes un email de "BancoX" con un enlace para "verificar tu cuenta":

1. **Revisas el remitente:** ¿Coincide con el dominio oficial?
2. **Inspeccionas el encabezado:** Usas MxToolbox para detectar inconsistencias.
3. **Pasas el enlace por VirusTotal:** Detecta que el dominio es nuevo y malicioso.
4. **No haces clic ni descargas nada.**
5. **Reportas el email a tu área de seguridad o proveedor.**

## Herramientas y sitios para análisis de phishing

### 1. Análisis de emails sospechosos

#### ● MxToolbox – Análisis de encabezados (headers)

**Sitio:** https://mxtoolbox.com/EmailHeaders.aspx\
**Uso:** Copiar y pegar encabezado completo del email para ver rutas, IPs, y autenticación SPF, DKIM, DMARC.

**Pasos:**

1. Obtener encabezado completo del email desde el cliente (Gmail, Outlook, Thunderbird).
2. Pegar en el campo del sitio.
3. Analizar la autenticidad del remitente.

***

#### ● CheckPhish

**Sitio:** [https://checkphish.ai](https://checkphish.ai)\
**Uso:** Revisión automática de URL o página sospechosa.

**Pasos:**

1. Ingresar la URL.
2. Observar resultado de análisis de phishing, redirecciones o clonación.

***

#### ● Mail Header Analyzer (Microsoft)

**Sitio:** https://mha.azurewebsites.net\
**Uso:** Análisis rápido de encabezados de correo.

***

### 2. Análisis de URLs

#### ● VirusTotal

**Sitio:** [https://virustotal.com](https://virustotal.com)\
**Uso:** Escanear archivos, URLs o dominios con múltiples motores antivirus.

**Pasos:**

1. Subir archivo o pegar enlace.
2. Observar resultados en pestañas `Detection`, `Details` y `Behavior`.

**Comando con API (requiere clave):**

```bash
bashCopyEditcurl --request GET \
  --url https://www.virustotal.com/api/v3/urls/{url_id} \
  --header 'x-apikey: TU_API_KEY'
```

***

#### ● URLVoid

**Sitio:** [https://urlvoid.com](https://urlvoid.com)\
**Uso:** Verificar reputación de dominios.

**Pasos:**

1. Ingresar dominio.
2. Revisar historial, blacklist, servidores, país, etc.

***

#### ● PhishTank

**Sitio:** [https://phishtank.org](https://phishtank.org)\
**Uso:** Comprobar si una URL está reportada como phishing.

***

### 3. Análisis de páginas web maliciosas

#### ● Burp Suite Community

**Sitio:** https://portswigger.net/burp\
**Uso:** Interceptar y analizar tráfico HTTP/HTTPS. Ideal para detectar redirecciones, formularios maliciosos y capturas de datos.

**Instalación en Linux:**

```bash
bashCopyEditsudo snap install burpsuite
```

**Pasos básicos:**

1. Configurar el proxy (127.0.0.1:8080) en el navegador.
2. Activar “Intercept” para ver peticiones salientes.
3. Usar "HTTP history" para navegar y analizar.

***

#### ● Wget y curl – Descarga y análisis rápido

**Wget ejemplo:**

```bash
bashCopyEditwget --no-check-certificate -p https://sitiofalso.com
```

**Curl ejemplo:**

```bash
bashCopyEditcurl -I https://sitiofalso.com
```

***

### 4. Análisis de archivos adjuntos

#### ● Cuckoo Sandbox

**Sitio:** [https://cuckoosandbox.org](https://cuckoosandbox.org)\
**Uso:** Análisis automático de malware (PDFs, EXEs, DOCs).\
**Requiere instalación en máquina Linux.**

**Instalación (resumida en Ubuntu):**

```bash
bashCopyEditsudo apt install cuckoo
cuckoo init
cuckoo -d
```

***

#### ● Any.Run (análisis online interactivo)

**Sitio:** [https://any.run](https://any.run)\
**Uso:** Entorno online para ejecutar y observar malware en tiempo real.

**Pasos:**

1. Subir archivo.
2. Esperar análisis dinámico.
3. Observar llamadas a red, procesos, cambios de registro, etc.

***

### 5. Comprobación de certificados SSL

#### ● SSL Labs

**Sitio:** https://www.ssllabs.com/ssltest\
**Uso:** Análisis completo del certificado SSL de una web sospechosa.

***

### 6. Herramientas CLI en Linux

#### ● host / dig – Verificar dominios

```bash
bashCopyEdithost sitio.com
dig sitio.com any
```

#### ● whois – Información de registro del dominio

```bash
bashCopyEditwhois sitio.com
```

#### ● nslookup – Consultas DNS básicas

```bash
bashCopyEditnslookup sitio.com
```

***

### 7. Checklists básicos

**Para emails:**

* Analizar encabezado (SPF/DKIM/DMARC).
* Verificar dominio del remitente.
* No abrir enlaces directamente.
* No descargar archivos adjuntos sin análisis.

**Para sitios web:**

* Verificar dominio exacto.
* Usar herramientas como VirusTotal y Burp.
* Inspeccionar certificados SSL.
* Verificar actividad sospechosa en el navegador (JS oculto, iframes, redirecciones).
