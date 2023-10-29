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

# Page Enumeration/ App Enumeration

Una vez que haya identificado que un servidor web se está ejecutando en un host de destino, el siguiente paso es echar un vistazo a la aplicación web y comenzar a mapear la superficie de ataque realizando una enumeración de páginas web o, a menudo, denominada enumeración de aplicaciones web. La práctica herramienta Nmap tiene un script NSE disponible para forzar brutalmente el directorio y las rutas de archivos de las aplicaciones web. Armado con una lista de archivos y directorios conocidos utilizados por aplicaciones web comunes, sondea el servidor en busca de cada uno de los elementos de la lista. En función de la respuesta del servidor, puede determinar si existen esas rutas. Esto es útil para identificar cosas como la página de administración predeterminada de Apache o Tomcat que comúnmente se dejan en los servidores web y pueden ser rutas potenciales para la explotación.

```
nmap -sV --script=http-enum -p 80 192.168.1.251
```

Nikto es un escáner de vulnerabilidades web de código abierto.No es tan robusto como los escáneres comerciales de vulnerabilidades web; sin embargo, es muy útil para ejecutar un script rápido para enumerar información sobre un servidor web y las aplicaciones que aloja. Debido a la velocidad a la que Nikto trabaja para escanear un servidor web, es muy ruidoso. Proporciona una serie de opciones para el escaneo, incluida la capacidad de autenticarse en una aplicación web que requiere un nombre de usuario y una contraseña.&#x20;

```
nikto -h 192.168.1.251
```
