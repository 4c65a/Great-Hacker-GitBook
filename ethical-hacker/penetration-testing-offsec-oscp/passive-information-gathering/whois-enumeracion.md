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
whois example.com -h 192.168.50.251
```

**Búsqueda inversa:**

Si tenemos una dirección IP, podemos usar whois para realizar una búsqueda inversa y obtener más información.

**Ejemplo:**

```
whois 38.100.193.70 -h 192.168.50.251
```
