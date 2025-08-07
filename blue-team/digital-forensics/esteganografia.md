# Esteganografía

## 📜 ¿Qué es la Esteganografía?

La **esteganografía** es el arte y la ciencia de **ocultar mensajes o información dentro de datos que no parecen contener nada secreto**. A diferencia de la criptografía, que cifra la información para hacerla ilegible, la esteganografía la esconde dentro de objetos cotidianos para que pase desapercibida.

**Ejemplo clásico:**\
Un archivo de texto con información secreta puede ocultarse dentro de un archivo de imagen. Si envías esta imagen por correo electrónico, para el destinatario será simplemente una imagen común. Sin embargo, con las herramientas adecuadas, puede recuperarse el archivo oculto.

También es común insertar mensajes secretos dentro de los **metadatos** de un archivo (datos sobre los datos, como autor, fecha, etc.).

> Para entender mejor, te recomiendo leer este artículo breve de TechTarget sobre Esteganografía.

***

## 🛠️ Steghide: herramienta práctica para esteganografía

### ¿Qué es Steghide?

**Steghide** es una herramienta en Linux, especialmente incluida en Kali Linux, que permite **ocultar archivos dentro de imágenes o audios** y también recuperarlos.

#### Instalación

Si no tienes Steghide instalado, en Kali Linux o Debian, ejecútalo:

```bash
bashCopyEditsudo apt-get install steghide
```

Confirma con `y` y espera la instalación.

***

### ⚙️ ¿Qué puede hacer Steghide?

* Permite ocultar un archivo secreto dentro de un archivo de portada (solo imágenes y archivos de audio).
* Protege el contenido oculto con contraseña para que sólo el destinatario autorizado pueda extraerlo.

***

### 🧩 Ejemplo práctico: ocultar un archivo ZIP dentro de una imagen

#### Paso 1: Preparar archivos

Tenemos:

* Archivo de portada: `laptop.jpg` (imagen)
* Archivo secreto: un archivo comprimido `secret.zip` que contiene un archivo `1.txt`

Si no tienes `secret.zip`, créalo así:

```bash
bashCopyEditzip -r secret.zip secret/
```

(donde `secret/` es la carpeta que contiene el archivo `1.txt`).

#### Paso 2: Incrustar el archivo secreto

```bash
bashCopyEditsteghide embed -cf laptop.jpg -ef secret.zip
```

* `embed`: modo para ocultar archivos
* `-cf laptop.jpg`: archivo de portada
* `-ef secret.zip`: archivo que quieres ocultar

Cuando te pregunte, ingresa una contraseña segura. Esta será necesaria para extraer el archivo después.

***

#### Alternativa: crear un nuevo archivo con el contenido oculto

Si no quieres sobrescribir el archivo original, usa la opción `-sf` para especificar un nuevo archivo:

```bash
bashCopyEditsteghide embed -cf laptop.jpg -ef secret.zip -sf laptop2.jpg
```

Así `laptop2.jpg` será el archivo con el ZIP oculto.

***

### 🕵️‍♂️ Cómo extraer el archivo oculto

Sabiendo que `laptop2.jpg` es un archivo Stego, y con la contraseña (por ejemplo, `password`), ejecutamos:

```bash
bashCopyEditsteghide extract -sf laptop2.jpg
```

Se te pedirá la contraseña, y luego Steghide extraerá el archivo oculto `secret.zip` al directorio actual.
