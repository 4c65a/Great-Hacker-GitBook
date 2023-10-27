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

# Recon-ng

Utilizado para la recopilación de información y reconocimiento de red automatizada. Es una herramienta que puede ser utilizada por profesionales de la seguridad, investigadores y cualquier persona que necesite obtener información sobre un objetivo.

Para iniciarlo utilizar el siguiente comando:

```
recon-ng
```

**Funciones básicas**

Recon-ng tiene una gran cantidad de funciones, pero algunas de las más básicas incluyen:

* **Workspaces:** Los workspaces le permiten almacenar configuraciones y datos para diferentes objetivos.
* **Modules:** Los módulos son scripts que realizan tareas específicas.
* **Database:** La base de datos almacena la información que recopila Recon-ng.

**Workspaces**

Un workspace es un conjunto de configuraciones y datos que se utilizan para un objetivo específico. Puede crear un nuevo workspace usando el siguiente comando:

```
recon-ng workspaces create [nombre_del_workspace]
```

Para cargar un workspace existente, use el siguiente comando:

```
recon-ng workspaces load [nombre_del_workspace]
```

**Modules**

Los módulos son scripts que realizan tareas específicas. Recon-ng tiene una amplia gama de módulos disponibles, que incluyen módulos para recopilar información de dominios, hosts, redes y personas, así como módulos para buscar vulnerabilidades y riesgos.

Para obtener una lista de todos los módulos disponibles, use el siguiente comando:

```
recon-ng modules list
```

Para ejecutar un módulo, use el siguiente comando:

```
recon-ng use [nombre_del_modulo]
```

**Database**

La base de datos almacena la información que recopila Recon-ng. Esto incluye información sobre dominios, hosts, redes y personas, así como información sobre vulnerabilidades y riesgos.

Para ver la información que se almacena en la base de datos, use el siguiente comando:

```
recon-ng db show
```
