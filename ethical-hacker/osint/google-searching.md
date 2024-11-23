# Google Searching

Técnica avanzada para realizar búsqueda más precisa en el navegador de Google, de este modo se realiza un reconocimiento pasivo del objetivo sin tener una interacción directa.\
Para realizar la búsqueda se suele usar distintos tipos de parámetros.

* **site:** Búsqueda a un sitio web, dominio o subdominio específico.\
  **Ejemplo**: `site:example.com`, `site:sub.example.com`
* **filetype:, ext:** Encuentra archivos específicos que puedan contener información sensible.\
  **Ejemplo**: `filetype:log`, `filetype:env`, `ext:sql`
* **inurl:, allinurl:** Busca URLs que contengan patrones interesantes, como rutas de inicio de sesión o archivos vulnerables.\
  **Ejemplo**: `inurl:login`, `allinurl:admin panel`
* **intitle:, allintitle:** Busca páginas con títulos que pueden indicar vulnerabilidades o áreas sensibles.\
  **Ejemplo**: `intitle:"Index of /"`, `allintitle:"admin dashboard"`
* **intext:, allintext:** Busca páginas cuyo contenido puede incluir información sensible.\
  **Ejemplo**: `intext:"password"`, `allintext:"confidential"`
* **link:** Encuentra páginas que enlazan a un dominio objetivo, útil para mapeo de red y análisis de reputación.\
  **Ejemplo**: `link:example.com`

***

#### Operadores avanzados

* **" ":** Encuentra coincidencias exactas en texto o URL, útil para localizar datos sensibles.\
  **Ejemplo**: `"admin password"`, `"config.php"`
* **OR, |:** Amplía la búsqueda para incluir resultados con cualquiera de los términos indicados.\
  **Ejemplo**: `"error log" OR "access denied"`
* **-:** Excluye términos no deseados de los resultados para mejorar la relevancia.\
  **Ejemplo**: `site:example.com -blog`
* **\*:** Usa un comodín para buscar patrones variados.\
  **Ejemplo**: `"index of * backup"`

**Sitios de Google Dorks.**

{% embed url="https://www.exploit-db.com/google-hacking-database" %}

{% embed url="https://pentest-tools.com/information-gathering/google-hacking" %}
