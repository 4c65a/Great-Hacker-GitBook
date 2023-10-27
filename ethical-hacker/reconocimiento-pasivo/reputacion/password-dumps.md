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

# Password dumps

Los atacantes pueden aprovechar los volcados de contraseñas de brechas anteriores. Hay varias formas en que un atacante puede obtener acceso a estos volcados de contraseñas, como mediante el uso de Pastebin, sitios web de la dark web e incluso GitHub en algunos casos. Varias herramientas y sitios web facilitan mucho esta tarea. Un ejemplo de una herramienta que le permite encontrar direcciones de correo electrónico y contraseñas expuestas en brechas anteriores es h8mail.

**Ejemplo 3-9. Instalación y uso de h8mail**

```
h8mail -t admin@evilcorp.com
```

Este comando buscará el correo electrónico `admin@evilcorp.com` en todos los volcados de contraseñas conocidos. Si se encuentra una coincidencia, h8mail mostrará la contraseña correspondiente.

**Se puede consultar a los siguientes sitios web:**&#x20;

* haveibeenpwned.com
* f-secure.com
* hacknotice.com
* breachdirectory.com
* keepersecurity.com
