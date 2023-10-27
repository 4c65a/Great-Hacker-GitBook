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

# Fallas criptográficas

Durante la fase de reconocimiento, los atacantes a menudo pueden inspeccionar los certificados SSL para obtener información sobre la organización, posibles fallas criptográficas e implementaciones débiles. Dentro de los certificados digitales se puede encontrar mucha información: el número de serie del certificado, el nombre común del sujeto, el URI del servidor al que se asignó, el nombre de la organización, la información del OCSP, el URI de la CRL, etc.

La revocación de certificados es el acto de invalidar un certificado digital. Por ejemplo, si una aplicación ha sido desmantelada o el certificado asignado a dicha aplicación está comprometido, se debe revocar el certificado y agregar su número de serie a una CRL. El OCSP y las CRL se utilizan para verificar si un certificado ha sido revocado (es decir, invalidado) por la autoridad emisora.

La figura 3-1 muestra el certificado digital asignado a h4cker.org. El certificado muestra la organización que emitió el certificado (en este caso, Let's Encrypt), el número de serie, el período de validez y la información de la clave pública, incluido el algoritmo, el tamaño de la clave, etc. Los atacantes pueden usar esta información para revelar cualquier configuración o implementación criptográfica débil.

**Recomendaciones para la seguridad de los certificados SSL:**

* Utilice certificados SSL emitidos por una autoridad de certificación (CA) de confianza.
* Asegúrese de que sus certificados SSL estén vigentes y que no hayan sido revocados.
* Configure sus servidores web para utilizar protocolos SSL seguros y robustos, como TLS 1.3.
* Mantenga su software actualizado, incluidos los certificados SSL.

Unas de las forma mas conocidas para verificar certificados es ir al sitio web [https://crt.sh/](https://crt.sh/)

<figure><img src="../../.gitbook/assets/2023-10-27_03-00.png" alt=""><figcaption></figcaption></figure>

| Herramienta | Descripción                                                             | Uso            |
| ----------- | ----------------------------------------------------------------------- | -------------- |
| sslscan     | Consulta los servicios SSL para determinar qué cifrados son compatibles | Reconocimiento |
| ssldump     | Analiza y decodifica el tráfico SSL                                     | Explotación    |
| sslh        | Ejecuta múltiples servicios en el puerto 443                            | Utilidad       |
| sslsplit    | Habilita los ataques MitM en conexiones de red cifradas con SSL         | Explotación    |
| sslyze      | Analiza la configuración SSL de un servidor conectándose a él           | Reconocimiento |

Unas de las formas para ver las certificaciones es usar :

**SSLScan es una herramienta  que se utiliza para escanear la configuración SSL de un servidor.**

**Escanear el dominio y guardar en un archivo .html**

```bash
sslscan skillsforall.com | aha > sfa_cert.html
```

**Escanear dominio**&#x20;

```
sslscan google.com
```

**Escanea una lista de dominios en un archivo**&#x20;

```
sslscan -t dominios.txt
```

**Escanea los puestos del servidor**

```
sslscan -d 192.168.1.1 -p 443
```

**Muestra información detallada**&#x20;

```
sslscan -d google.com -v
```

**Muestra información breve**

```
sslscan -d google.com -q
```

**Especifica una lista de cifrados**

```
sslscan -d google.com -c ciphers.txt
```

**Especifica una lista de protocolos**

| Protocol   | Comment                                                                                                                                                                                           |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SSL        | Enables TLS v1.0, v1.1, and v1.2 protocols.                                                                                                                                                       |
| SSLv3      | No protocols enabled.                                                                                                                                                                             |
| TLS        | Enables TLS v1.0, v1.1, v1.2, and v1.3 protocols.                                                                                                                                                 |
| TLSv1      | Enables TLS v1.0 protocol (defined in RFC 2246).                                                                                                                                                  |
| TLSv1.1    | Enables TLS v1.1 protocol (defined by RFC 4346).                                                                                                                                                  |
| TLSv1.2    | Enables TLS v1.2 protocol (defined by RFC 5246).                                                                                                                                                  |
| TLSv1.3    | Enables TLS v1.3 protocol (defined by RFC 8446).                                                                                                                                                  |
| SSL\_TLS   | Enables TLS v1.0 protocol.                                                                                                                                                                        |
| SSL\_TLSv2 | Enables TLS v1.0, v1.1, and v1.2 protocols.                                                                                                                                                       |
| SSLv2Hello | The SSLv3, TLSv1, TLSv1.1, and TLSv1.2 protocols allow you to send SSLv3, TLSv1, TLSv1.1, and TLSv1.2 ClientHellos encapsulated in an SSLv2 format hello by using the SSLv2Hello pseudo protocol. |

```
sslscan -d google.com -s protocols.txt
```

**Habilita el análisis avanzado**

```
sslscan -d google.com -a
```

**No muestra información sobre cifrados admitidos**

```
sslscan -d google.com -n
```

**Especifica un archivo que contiene un certificado de confianza**

```
sslscan -d google.com -k trust.pem
```

