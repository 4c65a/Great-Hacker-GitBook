# Cross-Site Scripting (XSS)

## Cross-Site Scripting (XSS)

Esta Unidad de Aprendizaje cubre los siguientes Objetivos de Aprendizaje:

* Comprender los tipos de vulnerabilidades de Cross-Site Scripting.
* Explotar Cross-Site Scripting básico.
* Realizar Escalada de Privilegios a través de Cross-Site Scripting.

Una de las características más importantes de una aplicación web bien defendida es la sanitización de datos, un proceso en el cual la entrada del usuario se procesa para eliminar o transformar todos los caracteres o cadenas peligrosas. Los datos no sanitizados permiten que un atacante inyecte y potencialmente ejecute código malicioso.

Cross-Site Scripting (XSS) es una vulnerabilidad que explota la confianza de un usuario en un sitio web al inyectar dinámicamente contenido en la página renderizada por el navegador del usuario.

En algún momento se pensó que XSS era una vulnerabilidad de riesgo relativamente bajo, pero hoy en día es de alto riesgo y prevalente, permitiendo que los atacantes inyecten scripts del lado del cliente, como JavaScript, en las páginas web visitadas por otros usuarios.

#### 8.4.1 Teoría de XSS Almacenado vs. Reflejado

Las vulnerabilidades XSS se pueden agrupar en dos clases principales: almacenado o reflejado.

**Almacenado XSS:**

Los ataques de XSS almacenado, también conocidos como XSS persistente, ocurren cuando la carga útil del exploit se almacena en una base de datos o en caché de alguna otra manera por un servidor. La aplicación web luego recupera esta carga útil y la muestra a cualquiera que visite una página vulnerable. Por lo tanto, una sola vulnerabilidad de XSS almacenado puede atacar a todos los usuarios del sitio. Estas vulnerabilidades a menudo existen en software de foros, especialmente en secciones de comentarios, en revisiones de productos o en cualquier lugar donde se pueda almacenar y revisar el contenido del usuario más tarde.

**Reflejado XSS:**

Los ataques de XSS reflejado generalmente incluyen la carga útil en una solicitud o enlace manipulado. La aplicación web toma este valor y lo coloca en el contenido de la página. Esta variante de XSS solo ataca a la persona que envía la solicitud o visita el enlace. Las vulnerabilidades de XSS reflejado a menudo pueden ocurrir en campos y resultados de búsqueda, así como en cualquier lugar donde la entrada del usuario se incluya en mensajes de error.

Cualquiera de estas dos variantes de vulnerabilidad puede manifestarse como del lado del cliente (navegador) o del servidor; también pueden ser basadas en DOM.

**XSS basado en DOM:**

El XSS basado en DOM ocurre únicamente dentro del Modelo de Objetos del Documento (DOM) de la página. Aunque no cubriremos demasiados detalles por ahora, debemos saber que los navegadores analizan el contenido HTML de una página y luego generan una representación interna del DOM. Este tipo de XSS ocurre cuando el DOM de una página se modifica con valores controlados por el usuario. El XSS basado en DOM puede ser almacenado o reflejado.
