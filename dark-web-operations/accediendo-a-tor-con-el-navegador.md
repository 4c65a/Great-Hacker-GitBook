# Accediendo a TOR con el navegador

## ¿Qué es TOR?

**TOR** (siglas de _The Onion Router_) es un software libre y de código abierto diseñado para **proteger la privacidad y el anonimato en línea**. Fue originalmente desarrollado por la Marina de los EE.UU. para proteger las comunicaciones gubernamentales, y hoy en día es mantenido por la comunidad bajo el **Proyecto TOR**.

***

## Web Clara vs. Web Oscura: ¿Cómo se diferencia?

#### Navegación convencional (Google Chrome, Firefox, etc.)

1. Escribes una URL (por ejemplo, `www.bbc.com`)
2. Tu **ISP (Proveedor de Internet)** ve esa solicitud
3. Esa solicitud se envía directamente al servidor del sitio web
4. El sitio puede rastrear tu IP, ubicación, cookies, historial, etc.

#### Navegación con TOR

1. Escribes una URL
2. TOR **cifra tu solicitud** y la envía a tu ISP
3. Luego rebota esa solicitud a través de **varios nodos TOR** (voluntarios alrededor del mundo)
4. Finalmente, se descifra en el nodo de salida y se envía al servidor destino



![Cómo funciona TOR](https://www.hotspotshield.com/imgs/resources/tor-vs-vpn/how-tor-works.png)

***

## Navegando por la Web Clara con TOR

Puedes usar TOR para navegar sitios normales como Google, BBC, Wikipedia, etc.

✔ Más privacidad\
✔ Sin rastreo de cookies\
✔ Historial borrado automáticamente\
✔ Uso de motores de búsqueda centrados en la privacidad (como **DuckDuckGo**)

🔍 Ejemplo: busca “BBC” y accede como siempre, pero con mayor anonimato.

***

## Navegando por la Web Oscura

**Acceder a sitios de la Dark Web con TOR**.

**Advertencia Crítica:**

La Dark Web contiene una gran cantidad de **contenido ilegal, perturbador o malicioso**. Además, **muchos sitios están diseñados para comprometer tu privacidad, robar tus datos o infectar tu sistema**.

> **Navega únicamente con fines educativos, de investigación o de threat intelligence**, y siempre en entornos controlados.

#### Acceso responsable con TOR:

* Utiliza el navegador **TOR** (The Onion Router) para acceder a sitios con dominio `.onion`.
* Asegura tu entorno:
  * Usa una **máquina virtual aislada** o un sistema tipo **Tails/Linux**.
  * Nunca accedas con tu IP real.
  * Desactiva JavaScript.
* Ingresa solo a **sitios verificados o de propósito legítimo** (por ejemplo, buscadores académicos, foros de análisis de amenazas, portales de periodistas o investigadores).

***

## Importante: Sitios `.onion` cambian con frecuencia

Dado que los dominios `.onion` son difíciles de recordar y pueden cambiar, muchos sitios son **temporales o migran** a nuevas URLs.\
No existe un "Google" oficial para buscar sitios `.onion`. Existen índices y catálogos, pero muchos contienen enlaces maliciosos.

