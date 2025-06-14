# Tipos de evidencia

### **¿Qué es la evidencia digital?**

La evidencia digital es **cualquier información almacenada, transmitida o recibida** en dispositivos electrónicos que pueda ser relevante en una investigación. Con la proliferación de dispositivos como computadoras, móviles, IoT, consolas y servidores, **casi cualquier equipo puede contener evidencia potencial**.

#### **Tipos principales de evidencia digital**

1. **Evidencia en computadoras**
   * Incluye archivos, correos electrónicos, chats, imágenes, videos y documentos almacenados en discos duros.
   * También puede estar oculta mediante técnicas como la esteganografía o en el espacio libre del disco.
   * Es fundamental para casos internos (como investigaciones laborales) o judiciales.
2. **Evidencia en redes**
   * Se obtiene del historial de navegación, proxies, routers o registros de actividad web.
   * Permite identificar accesos indebidos, navegación inapropiada o violaciones de políticas internas.
   * Las redes sociales, foros, blogs y aplicaciones de mensajería también pueden aportar pruebas legales.
3. **Evidencia en dispositivos móviles**
   * Teléfonos y tablets contienen un volumen enorme de datos útiles: llamadas, mensajes, ubicación GPS, apps, imágenes, etc.
   * Incluso se pueden recuperar datos eliminados con herramientas especializadas.
   * Son una fuente clave en investigaciones modernas por su uso cotidiano.

### **Cadena de Custodia en Evidencia Digital**

#### ¿Qué es?

La **Cadena de Custodia** es el **proceso riguroso y documentado** mediante el cual se recolecta, manipula y almacena evidencia (física o digital) **para asegurar su integridad** y validez en un procedimiento legal.

***

#### **Objetivo principal**

Garantizar que la **evidencia no sea alterada**, contaminada ni manipulada desde su recolección hasta su presentación en juicio.

***

#### **Elementos que se deben registrar**

* **Recibido de** (quién entregó la evidencia)
* **Recibido por** (quién la recibió)
* **Fecha**
* **Hora**

***

#### **Buenas prácticas del analista forense**

1. **Nunca trabajar con la evidencia original**
   * Se crea una **imagen forense** del disco.
   * Se calcula un **hash** (ej. SHA256) antes y después de la copia.
   * Si los hashes coinciden, se verifica que la copia es exacta.
2. **Trabajo siempre sobre la copia**
   * Protege la evidencia original para garantizar su integridad legal.
3. **Uso de discos forenses limpios**
   * Todo medio donde se copiará la evidencia debe estar **previamente desinfectado** (sin datos anteriores).
   * Esto **evita contaminación** de la evidencia.

***

#### **Importancia**

Si no se respeta la cadena de custodia, **la evidencia puede ser rechazada en juicio**, lo que compromete la investigación y puede beneficiar al acusado.

### **CLI de Linux: Lectura de archivos y detección de extensiones falsas**

#### 🔹 Introducción

En esta sección aprenderás dos habilidades esenciales para el análisis forense y la ciberseguridad:

1. **Leer el contenido de archivos usando la terminal.**
2. **Detectar y corregir extensiones de archivo manipuladas.**

***

### 📁 **Parte 1: Identificación de extensiones incorrectas**

Es común que un archivo tenga **una extensión falsa** para ocultar su verdadera naturaleza. Un archivo puede llamarse `imagen.jpeg`, pero en realidad ser un archivo `.zip`, `.exe`, o incluso un malware. Veremos cómo detectarlo y restaurarlo a su formato correcto.

#### 🔍 **Caso práctico:**

Supongamos que encontramos dos archivos:

* `foto1.jpeg`
* `foto2.zip`

Queremos analizar `foto2.zip`.

1. **Intentamos descomprimirlo:**

```bash
bashCopyEditunzip foto2.zip
```

Esto **genera un error**: “End-of-central-directory signature not found”. El sistema nos dice que **no es realmente un archivo ZIP**.

2. **Usamos el comando `file`:**

```bash
bashCopyEditfile foto2.zip
```

Salida del sistema:

```
arduinoCopyEditfoto2.zip: JPEG image data, JFIF standard
```

El archivo es en realidad una **imagen JPEG**, pero tiene la extensión `.zip`.

3. **Solución: renombrarlo correctamente:**

```bash
bashCopyEditmv foto2.zip foto2.jpeg
```

Ahora el archivo puede ser abierto correctamente y su miniatura aparece en el entorno gráfico.

> ⚠️ _Importante en ciberseguridad:_ Muchos atacantes ocultan malware renombrando archivos ejecutables como si fueran imágenes, PDFs o archivos de texto. Siempre verifica con `file`.

***

### 📖 **Parte 2: Lectura de contenido de archivos desde la terminal**

Una vez que te mueves entre carpetas con `cd` y ves archivos con `ls`, el siguiente paso es **leer su contenido** sin abrir un editor. Para ello usamos tres comandos fundamentales:

***

#### 📘 **1. `strings` – Leer texto legible en archivos binarios o mixtos**

Este comando **extrae y muestra todas las cadenas legibles** (texto visible) de un archivo, incluso si no es un archivo de texto puro.

**Ejemplo:**

```bash
bashCopyEditstrings archivo_misterioso
```

Ideal para inspeccionar imágenes, ejecutables o archivos de audio que podrían contener **mensajes ocultos**.

***

#### 📗 **2. `cat` – Mostrar todo el contenido del archivo**

Este comando muestra **todo el contenido**, incluyendo líneas que no son detectadas por `strings`.

**Ejemplo:**

```bash
bashCopyEditcat notas_secretas.txt
```

A diferencia de `strings`, también muestra líneas codificadas o caracteres especiales.

***

#### 📕 **3. `head` – Mostrar solo las primeras líneas**

Muestra por defecto las **primeras 10 líneas** de un archivo, útil para archivos largos.

**Ejemplo:**

```bash
bashCopyEdithead registro.log
```

También puedes personalizar cuántas líneas mostrar:

```bash
bashCopyEdithead -n 20 registro.log
```

***

#### 🧠 **Ejemplo completo: inspeccionando un archivo sospechoso**

Tienes un archivo llamado `mensaje.jpeg`. Quieres saber si contiene texto oculto:

1. **Comprueba su tipo real:**

```bash
bashCopyEditfile mensaje.jpeg
```

2. **Busca texto oculto:**

```bash
bashCopyEditstrings mensaje.jpeg
```

3. **Confirma todo el contenido:**

```bash
bashCopyEditcat mensaje.jpeg
```

Si obtienes líneas sospechosas (por ejemplo, frases como `"clave: 1234"` o `"oculto aquí"`), ya sabes que hay que investigarlo más a fondo.
