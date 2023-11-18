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

```
nikto
```

**Parte 2: Utilice Nikto para escanear varios servidores web**

```
nikto -h google.com
```

**Parte 3: Investigar las vulnerabilidades del sitio web**

* **Comando para escanear varias direcciones IP desde un archivo:** `nikto -h IP_list.txt`

**Parte 4: Exportar resultados de Nikto a un archivo**

* **Comando para exportar resultados a un archivo HTML:** `nikto -h 172.17.0.2 -o scan_results.htm`
* **Comando para exportar resultados a un archivo de texto CSV:** `nikto -h 172.17.0.2 -o scan_results.txt -Formato csv`
