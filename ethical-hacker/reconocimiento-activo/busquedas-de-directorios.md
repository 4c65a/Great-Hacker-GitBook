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

# Busquedas de directorios

**La busqueda de directorios se puede hacer con varias herramientas.**

## Gobuster

El modo DIR se utiliza para buscar directorios y archivos ocultos.

```
gobuster dir -u https://google.com -w /wordlists/Discovery/Web-Content/common.txt  
```

`--delay 1s`, si los subprocesos están configurados en 4 y --delay en 1 s, esto enviará 4 solicitudes por segundo.

```
gobuster dir -u https://example.com -w /wordlists/Discovery/Web-Content/big.txt -t 4 --delay 1s -o resultados.txt
```

Esto es para cuando se especifica una búsqueda de extensión o extensiones de archivo específicas. `-x .php`

```
gobuster dir -u https://example.com -w /wordlists/Discovery/Web-Content/big.txt -x .php, .txt -t 4 --delay 1s -o results.txt
```

Para excluir códigos de estado utilice `-n`&#x20;

```
gobuster dir -u https://example.com -w /wordlists/Discovery/Web-Content/big.txt -n -t 4 --delay 1s -o results.txt
```





<mark style="color:red;">**Recursos**</mark>

{% embed url="https://byte-mind.net/enumeracion-por-fuerza-bruta-con-gobuster/" %}

{% embed url="https://github.com/OJ/gobuster" %}
