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

# Evaluación de aplicaciones web

### **Fingerprinting de Servidores Web con Nmap**

```bash
sudo nmap -p80 -sV 192.168.50.20
```

El resultado del escaneo muestra que el servidor Apache versión 2.4.41 está en ejecución en el host Ubuntu.

```bash
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
```

Para llevar nuestra enumeración más allá, utilizamos scripts específicos de Nmap para servicios, como http-enum, que realiza una huella inicial del servidor web.

```bash
sudo nmap -p80 --script=http-enum 192.168.50.20
```

El resultado del script http-enum muestra varias carpetas interesantes que podrían llevar a más detalles sobre la aplicación web del objetivo.

```bash
PORT   STATE SERVICE
80/tcp open  http
| http-enum:
|
/login.php: Possible admin folder
|
/db/: BlogWorx Database
|
/css/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)'
|
/db/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)'
|
/images/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)'
|
/js/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)'
|_ /uploads/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)'
```

Al usar scripts de Nmap, logramos descubrir información más específica de la aplicación que podemos agregar a la enumeración del servidor web que realizamos anteriormente.

### **Identificación de la Pila Tecnológica con Wappalyzer**

Junto con la recopilación activa de información que realizamos mediante Nmap, también podemos obtener pasivamente una gran cantidad de información sobre la pila tecnológica de la aplicación a través de Wappalyzer.

### **Fuerza Bruta de Directorios con Gobuster**

Una vez que hemos descubierto una aplicación en ejecución en un servidor web, nuestro siguiente paso es mapear todos sus archivos y directorios accesibles públicamente. Para hacer esto, necesitamos realizar múltiples consultas contra el objetivo para descubrir cualquier ruta oculta.&#x20;

> Debido a su naturaleza de fuerza bruta, Gobuster puede generar bastante tráfico, lo que no será útil cuando sea necesario pasar desapercibido.

Gobuster admite diferentes modos de enumeración, incluidos fuzzing y dns,que enumera archivos y directorios. Necesitamos especificar la IP del objetivo con el parámetro -u y una lista de palabras con -w. El número predeterminado de hilos en ejecución es 10; podemos reducir la cantidad de tráfico estableciendo un número menor a través del parámetro -t.

```bash
gobuster dir -u 192.168.50.20 -w /usr/share/wordlists/dirb/common.txt -t 5
```

### Burt Suite&#x20;

Es una plataforma integral basada en una interfaz gráfica de usuario (GUI) utilizada para realizar pruebas de seguridad en aplicaciones web. Desarrollada por PortSwigger, Burp Suite ofrece varias herramientas que permiten a los profesionales de seguridad evaluar la seguridad de las aplicaciones web, identificar vulnerabilidades y realizar pruebas de penetración.

Algunas de las características clave de Burp Suite incluyen:

1. **Proxy Web:** Permite interceptar y modificar las solicitudes y respuestas entre el navegador web y la aplicación web.
2. **Escáner de Vulnerabilidades:** Realiza análisis automatizado en busca de posibles vulnerabilidades en la aplicación web, como inyecciones SQL, ataques de fuerza bruta, entre otros.
3. **Spider:** Explora la aplicación web para mapear su estructura y descubrir posibles puntos de entrada.
4. **Repeater:** Facilita la repetición y modificación de solicitudes HTTP para probar y verificar vulnerabilidades.
5. **Secuencia de trabajo:** Proporciona un conjunto de herramientas integradas para diversos aspectos de pruebas de seguridad.
6. **Intruder:** Facilita la automatización de ataques de fuerza bruta o de diccionario para evaluar la resistencia de contraseñas u otras características de seguridad.

**Enumeración de Aplicaciones Web**

Esta Unidad de Aprendizaje aborda los siguientes Objetivos de Aprendizaje:

* Aprender a depurar el código fuente de una aplicación web.
* Comprender cómo enumerar e inspeccionar encabezados, cookies y código fuente.
* Aprender a llevar a cabo metodologías de prueba de API.

En un Módulo anterior, aprendimos cómo la recopilación de información de manera pasiva puede desempeñar un papel crítico al mapear aplicaciones web, especialmente cuando repositorios públicos o búsquedas en Google revelan información sensible sobre nuestro objetivo. Ya sea al trabajar con credenciales filtradas o simplemente documentación de la aplicación, siempre debemos hacer referencia a la información recuperada de manera pasiva durante nuestras pruebas activas de aplicaciones web, ya que podría llevarnos por caminos inexplorados.

Es importante identificar los componentes que conforman una aplicación web antes de intentar explotarla a ciegas. Muchas vulnerabilidades de aplicaciones web son agnósticas a la tecnología. Sin embargo, algunos exploits y payloads deben ser diseñados según los fundamentos tecnológicos de la aplicación, como el software de base de datos o el sistema operativo. Antes de lanzar cualquier ataque a una aplicación web, deberíamos intentar descubrir la pila tecnológica en uso. Las pilas tecnológicas generalmente constan de un sistema operativo host, software de servidor web, software de base de datos y un lenguaje de programación de frontend/backend.

Una vez que hayamos enumerado la pila subyacente utilizando las metodologías que aprendimos anteriormente, avanzaremos hacia la enumeración de la aplicación.

Podemos aprovechar varias técnicas para recopilar esta información directamente desde el navegador. La mayoría de los navegadores modernos incluyen herramientas de desarrollo que pueden ayudar en el proceso de enumeración.

Como sugiere el nombre, aunque las Herramientas de Desarrollo se utilizan típicamente por desarrolladores, son útiles para nuestros propósitos porque ofrecen información sobre el funcionamiento interno de nuestra aplicación objetivo.

Nos centraremos en Firefox, ya que es el navegador predeterminado en Kali Linux. Sin embargo, la mayoría de los navegadores incluyen herramientas similares.

**8.3.1 Depuración del Contenido de la Página**

Un buen lugar para comenzar nuestro mapeo de información de aplicaciones web es con una dirección URL. Las extensiones de archivos, que a veces forman parte de una URL, pueden revelar el lenguaje de programación en el que se escribió la aplicación. Algunas extensiones, como .php, son directas, pero otras son más crípticas y varían según los frameworks utilizados. Por ejemplo, una aplicación web basada en Java podría usar .jsp, .do o .html.

Las extensiones de archivos en las páginas web son cada vez menos comunes, sin embargo, ya que muchos lenguajes y marcos ahora admiten el concepto de rutas, que permiten a los desarrolladores asignar un URI a una...\
