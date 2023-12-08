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

# Open Sourcer code

**Recopilación de información pasiva de código en línea**

Esto incluye proyectos de código abierto y repositorios de código en línea como GitHub, GitHub Gist, GitLab y SourceForge.

El código almacenado en línea puede proporcionar una idea de los lenguajes de programación y marcos utilizados por una organización. En algunas ocasiones, los desarrolladores incluso han comprometido accidentalmente datos confidenciales y credenciales en repositorios públicos.

Las herramientas de búsqueda de algunas de estas plataformas admitirán los operadores de búsqueda de Google ,la búsqueda de GitHub. Podemos usar GitHub para buscar los repositorios de un usuario u organización.

Este enfoque manual funcionará mejor en repositorios pequeños. Para repositorios más grandes, podemos usar varias herramientas para ayudar a automatizar parte de la búsqueda, como Gitrob y Gitleaks. La mayoría de estas herramientas requieren un token de acceso para usar la API del proveedor de alojamiento de código fuente.

Las herramientas que buscan secretos en el código fuente, como Gitrob o Gitleaks, generalmente se basan en expresiones regulares o detecciones basadas en entropía para identificar información potencialmente útil**.** La detección basada en entropía intenta encontrar cadenas generadas aleatoriamente. La idea es que una cadena larga de caracteres y números aleatorios probablemente sea una contraseña. No importa cómo una herramienta busque secretos, ninguna herramienta es perfecta y se perderán cosas que una inspección manual podría encontrar.

**Algunas herramientas y recursos en línea que podemos usar para recopilar información de forma pasiva:**

* GitHub
* GitHub Gist
* GitLab
* SourceForge
