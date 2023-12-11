# Evaluación de aplicaciones web

**Fingerprinting de Servidores Web con Nmap**

Como se cubrió en un módulo anterior, Nmap es la herramienta principal para la enumeración activa inicial. Deberíamos comenzar la enumeración de aplicaciones web desde su componente principal, el servidor web, ya que este es el denominador común de cualquier aplicación web que expone sus servicios.

Dado que encontramos el puerto 80 abierto en nuestro objetivo, podemos proceder con el descubrimiento de servicios. Para empezar, confiaremos en el escaneo de servicios de nmap (-sV) para obtener el banner del servidor web (-p80).

```bash
kali@kali:~$ sudo nmap -p80 -sV 192.168.50.20
```

El resultado del escaneo muestra que el servidor Apache versión 2.4.41 está en ejecución en el host Ubuntu.

```bash
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
```

Para llevar nuestra enumeración más allá, utilizamos scripts específicos de Nmap para servicios, como http-enum, que realiza una huella inicial del servidor web.

```bash
kali@kali:~$ sudo nmap -p80 --script=http-enum 192.168.50.20
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

Como se muestra anteriormente, descubrimos varias carpetas interesantes que podrían proporcionar más detalles sobre la aplicación web del objetivo.

Al usar scripts de Nmap, logramos descubrir información más específica de la aplicación que podemos agregar a la enumeración del servidor web que realizamos anteriormente.

**Identificación de la Pila Tecnológica con Wappalyzer**

Junto con la recopilación activa de información que realizamos mediante Nmap, también podemos obtener pasivamente una gran cantidad de información sobre la pila tecnológica de la aplicación a través de Wappalyzer.

Una vez que hemos registrado una cuenta gratuita, podemos realizar una búsqueda de tecnología en el dominio megacorpone.com.

A partir de este rápido análisis externo de terceros, aprendimos sobre el sistema operativo, el marco de UI, el servidor web y más. Los resultados también proporcionan información sobre las bibliotecas de JavaScript utilizadas por la aplicación web; esto puede ser información valiosa, ya que algunas versiones de las bibliotecas de JavaScript son conocidas por verse afectadas por varias vulnerabilidades.

**Fuerza Bruta de Directorios con Gobuster**

Una vez que hemos descubierto una aplicación en ejecución en un servidor web, nuestro siguiente paso es mapear todos sus archivos y directorios accesibles públicamente. Para hacer esto, necesitamos realizar múltiples consultas contra el objetivo para descubrir cualquier ruta oculta. Gobuster es una herramienta (escrita en el lenguaje Go) que puede ayudarnos con este tipo de enumeración. Utiliza listas de palabras para descubrir directorios y archivos en un servidor mediante fuerza bruta.

Debido a su naturaleza de fuerza bruta, Gobuster puede generar bastante tráfico, lo que no será útil cuando sea necesario pasar desapercibido.

Gobuster admite diferentes modos de enumeración, incluidos fuzzing y dns, pero por ahora solo nos basaremos en el modo dir, que enumera archivos y directorios. Necesitamos especificar la IP del objetivo con el parámetro -u y una lista de palabras con -w. El número predeterminado de hilos en ejecución es 10; podemos reducir la cantidad de tráfico estableciendo un número menor a través del parámetro -t.

```bash
bashCopy codekali@kali:~$ gobuster dir -u 192.168.50.20 -w /usr/share/wordlists/dirb/common.txt -t 5
```

En la salida, vemos que Gobuster ha encontrado diez recursos. Cuatro de estos recursos no son accesibles debido a privilegios insuficientes (Estado: 403). Sin embargo, los seis restantes son accesibles y merecen una investigación más detallada.
