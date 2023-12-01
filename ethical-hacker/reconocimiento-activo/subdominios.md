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

# Subdominios

La busquedas de subdominos,son muy importante a la hora de hacer una auditoria de pentesting o bug bounty ,generalmente las empresas muestra el alcance de los dominios.



<img src="../../.gitbook/assets/file.excalidraw.svg" alt="" class="gitbook-drawing">

Existen varias forma de buscar subdominos tanto de forma pasiva o activa.

**De forma activa:**

```
subfinder -d example.com >> subdominios.txt
```

```
sublist3r -d example.com  >> subdominios.txt
```

```
amass enum -d example.com -max-dns-queries 120 >> subdominios.txt
```

```
amass enum -passive -d example.com >> subdominios.txt
```

