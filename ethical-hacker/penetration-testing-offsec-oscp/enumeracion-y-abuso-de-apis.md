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

# Enumeración y Abuso de APIs

En muchos casos, nuestro objetivo de prueba de penetración es una aplicación web de origen cerrado, construida internamente y que se suministra con una serie de Interfaces de Programación de Aplicaciones (API). Estas APIs son responsables de interactuar con la lógica del back-end y proporcionar una base sólida de funciones para la aplicación web.

Un tipo específico de API llamado Representational State Transfer (REST) se utiliza para una variedad de propósitos, incluida la autenticación.

En un escenario típico de prueba de caja blanca, recibiríamos documentación completa de la API para ayudarnos a mapear completamente la superficie de ataque. Sin embargo, al realizar una prueba de caja negra, tendremos que descubrir la API del objetivo nosotros mismos.

\
**Enumeración y Ataque de APIs con Gobuster**

Podemos utilizar las características de Gobuster para realizar un ataque de fuerza bruta en los puntos finales de la API. En este escenario de prueba, nuestro servidor web de la puerta de enlace de la API está escuchando en el puerto 5001 en la dirección IP 192.168.50.16, por lo que podemos intentar un ataque de fuerza bruta en directorios.

Las rutas de la API a menudo van seguidas de un número de versión, resultando en un patrón como: `/api_nombre/v1` **Listado 105 - Convención de Nomenclatura de Rutas de la API**

El nombre de la API suele ser bastante descriptivo sobre la función o los datos que utiliza para operar, seguido directamente por el número de versión.

Con esta información, intentemos realizar un ataque de fuerza bruta en las rutas de la API utilizando una lista de palabras junto con la función de patrones de Gobuster. Podemos llamar a esta función utilizando la opción `-p` y proporcionando un archivo con patrones. Para nuestra prueba, crearemos un archivo de patrones simple en nuestro sistema Kali que contenga el siguiente texto:

```bash
bashCopy code{GOBUSTER}/v1
{GOBUSTER}/v2
```

**Listado 106 - Patrón de Gobuster**

En este ejemplo, estamos utilizando el marcador de posición "{GOBUSTER}" para que coincida con cualquier palabra de nuestra lista de palabras, que se añadirá con el número de versión. Para mantener nuestra prueba simple, probaremos solo con dos versiones.

Ahora estamos listos para enumerar la API con Gobuster usando el siguiente comando:

```bash
bashCopy codekali@kali:~$ gobuster dir -u http://192.168.50.16:5002 -w /usr/share/wordlists/dirb/big.txt -p pattern
```

**Listado 107 - Enumeración de Rutas de la API con Gobuster**

Hemos descubierto múltiples coincidencias, incluyendo dos entradas interesantes que parecen ser puntos finales de la API, `/books/v1` y `/users/v1`.

**Acceso a la Documentación Completa de las APIs**

Si navegamos a la ruta `/ui`, descubriremos la documentación completa de las API. Aunque esto es común durante las pruebas de caja blanca, no es un lujo que normalmente tengamos durante una prueba de caja negra.

Primero, inspeccionemos la API `/users` con curl.

```bash
kali@kali:~$ curl -i http://192.168.50.16:5002/users/v1
```

**Listado 108 - Obtención de Información de Usuarios**

La aplicación devolvió tres cuentas de usuario, incluida una cuenta administrativa que parece valer la pena investigar más a fondo. Podemos utilizar esta información para intentar otro ataque de fuerza bruta con Gobuster, esta vez apuntando al usuario administrador con una lista de palabras más pequeña. Para verificar si alguna propiedad adicional de la API está relacionada con la propiedad del nombre de usuario, ampliaremos la ruta de la API insertando el nombre de usuario admin al final.

```bash
kali@kali:~$ gobuster dir -u http://192.168.50.16:5002/users/v1/admin/ -w /usr/share/wordlists/dirb/small.txt
```

**Listado 109 - Ataque de Fuerza Bruta Adicional en la Propiedad de Usuario Administrador**

Hemos iniciado Gobuster para realizar una enumeración de directorios en la ruta ampliada de la API. Este ataque puede ayudarnos a descubrir posibles propiedades o recursos adicionales relacionados con el usuario administrador.

El camino de la API de contraseñas parece atractivo para nuestros propósitos de prueba, así que lo probaremos mediante curl.

```
curl -i http://192.168.50.16:5002/users/v1/admin/password
```
