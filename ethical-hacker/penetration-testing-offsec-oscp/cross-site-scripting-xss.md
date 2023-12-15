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
