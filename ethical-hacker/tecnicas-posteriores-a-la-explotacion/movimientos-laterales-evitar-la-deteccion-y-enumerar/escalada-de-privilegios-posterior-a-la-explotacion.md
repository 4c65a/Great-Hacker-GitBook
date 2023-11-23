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

# Escalada de privilegios posterior a la explotación

### **Escalada de privilegios verticales**

Con la escalada de privilegios vertical,un usuario con privilegios más bajos accede a funciones reservadas para usuarios con privilegios más altos como acceso root o administrador.\
\
**Escalamiento de privilegios vertical.**

<img src="../../../.gitbook/assets/file.excalidraw.svg" alt="" class="gitbook-drawing">

### Escalada de privilegios horizontales

Con la escalada de privilegios horizontal,un usuario normal accede a funciones o contenido reservado para otros usuarios que no son root ni administradores.&#x20;

Por ejemplo, digamos que después de explotar un sistema, puede obtener acceso al shell como usuario omar. Sin embargo, ese usuario no tiene permisos para leer algunos archivos en el sistema. Luego descubre que otro usuario, hannah, tiene acceso a esos archivos. Luego encontrará una manera de aumentar sus privilegios como usuario hannah para acceder a esos archivos.\
\
**Escalamiento de privilegios horizontal.**

<img src="../../../.gitbook/assets/file.excalidraw (1).svg" alt="" class="gitbook-drawing">
