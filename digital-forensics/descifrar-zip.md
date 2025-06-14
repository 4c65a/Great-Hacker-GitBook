# Descifrar ZIP

## 🔐 Cómo proteger un archivo ZIP con contraseña

Para proteger un archivo ZIP con contraseña en Linux (por ejemplo, Debian o Kali), usa el comando `zip` con la opción `--encrypt`:

```bash
bashCopyEditzip --encrypt Protected.zip text.txt
```

* `zip`: programa para crear archivos comprimidos ZIP
* `--encrypt`: activa el cifrado y la solicitud de contraseña
* `Protected.zip`: nombre del archivo ZIP resultante
* `text.txt`: archivo que quieres comprimir y proteger

Cuando alguien intente extraer los archivos, el sistema pedirá la contraseña.

***

## 🕵️‍♂️ Cómo descifrar archivos ZIP protegidos

En el análisis forense, es común encontrar ZIP protegidos con contraseña que bloquean evidencia importante. Para descifrarlos, existen métodos como:

***

### 1. Ataques de fuerza bruta

* Prueba **todas las combinaciones posibles** de caracteres hasta encontrar la contraseña correcta.
* **Ventaja:** siempre funciona si se tiene tiempo y recursos suficientes.
* **Desventaja:** puede tardar muchísimo tiempo, especialmente si la contraseña es larga o compleja.

***

### 2. Ataques de diccionario

* Prueba contraseñas basadas en una lista común de palabras o contraseñas usadas frecuentemente (diccionario).
* **Ventaja:** mucho más rápido si la contraseña es sencilla o común.
* **Desventaja:** si la contraseña no está en el diccionario, no funcionará.

***

## ⚙️ Herramienta práctica: `fcrackzip`

En Kali o Debian, instala `fcrackzip` para intentar descifrar ZIP protegidos:

```bash
bashCopyEditsudo apt-get install fcrackzip
```

***

### Uso de `fcrackzip` para fuerza bruta

```bash
bashCopyEditfcrackzip -b -c a1 -l 4-6 -u archivo.zip
```

* `-b`: modo fuerza bruta
* `-c a1`: conjunto de caracteres a probar (letras minúsculas + números)
* `-l 4-6`: longitud de la contraseña (mínimo 4, máximo 6)
* `-u`: intenta extraer archivos para verificar contraseña correcta
* `archivo.zip`: archivo objetivo

***

### Uso de `fcrackzip` para ataque de diccionario

```bash
bashCopyEditfcrackzip -D -u -p /usr/share/wordlists/rockyou.txt archivo.zip
```

* `-D`: modo diccionario
* `-u`: verifica extrayendo
* `-p`: ruta al archivo con lista de contraseñas (como `rockyou.txt`)
* `archivo.zip`: archivo protegido a descifrar

