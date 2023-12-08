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

# Whois enumeracion

**La enumeración Whois es una técnica de reconocimiento pasivo.**

**¿Qué es Whois?**

Whois es un servicio TCP, herramienta y tipo de base de datos que puede proporcionar información sobre un nombre de dominio, como servidor de nombres y registrador. Esta información a menudo es pública, ya que los registradores cobran una tarifa por la registración privada.

**Recopilación de información básica del dominio**

Podemos recopilar información básica sobre un nombre de dominio ejecutando una búsqueda estándar y pasando el nombre de dominio (por ejemplo, megacorpone.com) a whois, proporcionando la dirección IP de nuestro servidor Whois de Ubuntu como argumento del parámetro host (-h).

**Ejemplo:**

```
kali@kali:$ whois megacorpone.com -h 192.168.50.251
```

**Salida:**

```
Domain Name: MEGACORPONE.COM
Registry Domain ID: 1775445745_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.gandi.net
Registrar URL: http://www.gandi.net
Updated Date: 2019-01-01T09:45:03Z
Creation Date: 2013-01-22T23:01:00Z
Registry Expiry Date: 2023-01-22T23:01:00Z
...
Registry Registrant ID: <Redacted>
Registrant Name: Alan Grofield
Registrant Organization: MegaCorpOne
Registrant Street: 2 Old Mill St
Registrant City: Rachel
Registrant State/Province: Nevada
Registrant Postal Code: 89001
Registrant Country: US
Registrant Phone: +1.9038836342
...
Registry Admin ID: <Redacted>
Admin Name: Alan Grofield
Admin Organization: MegaCorpOne
Admin Street: 2 Old Mill St
Admin City: Rachel
Admin State/Province: Nevada
Admin Postal Code: 89001
Admin Country: US
Admin Phone: +1.9038836342
...
Registry Tech ID: <Redacted>
Tech Name: Alan Grofield
Tech Organization: MegaCorpOne
Tech Street: 2 Old Mill St
Tech City: Rachel
Tech State/Province: Nevada
Tech Postal Code: 89001
Tech Country: US
Tech Phone: +1.9038836342
...
Name Server: NS1.MEGACORPONE.COM
Name Server: NS2.MEGACORPONE.COM
Name Server: NS3.MEGACORPONE.COM
...
```

**Información útil:**

No toda esta información es útil, pero descubrimos algunos datos valiosos:

* **Registrante:** Alan Grofield
* **Organización:** MegaCorpOne
* **Servidor de nombres:** NS1.MEGACORPONE.COM, NS2.MEGACORPONE.COM, NS3.MEGACORPONE.COM

**Búsqueda inversa:**

Si tenemos una dirección IP, podemos usar whois para realizar una búsqueda inversa y obtener más información.

**Ejemplo:**

```
kali@kali:$ whois 38.100.193.70 -h 192.168.50.251
```

**Salida:**

```
...
NetRange: 38.0.0.0 - 38.255.255.255
CIDR: 38.0.0.0/8
NetName: COGENT-A
...
OrgName: PSINet, Inc.
OrgId: PSI
Address: 2450 N Street NW
City: Washington
StateProv: DC
PostalCode: 20037
Country: US
RegDate: <Redacted>
Updated: 2015-06-04
...
```

**Información útil:**

* **Propietario de la IP:** PSINet, Inc.
