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

# Tratamiento de la TTY

Realizaremos una pequeña explicación del tratamiento de la terminal que hacemos siempre en todas las máquinas una vez conseguimos la reverse shell.

El motivo de esto, es que cuando ganamos acceso a la máquina, veremos que no podemos usar el backspace, las flechas, el tab para completar rutas… e incluso ni podremos utilizar servicios, como Python por ejemplo. Para terminar, si algo no va bien o pulsamos _Ctrl+C_ se nos cerrará la conexión. Queda claro que es casi imprescindible hacer este tratamiento en cuanto podamos.

Existen 2 formas (hay más, pero al menos yo no las uso):

1. `script /dev/null -c bash`
2. `python3 -c 'import pty;pty.spawn("/bin/bash")'`

Una vez hemos ejecutado una de estas “consolas”, debemos pulsar _Ctrl+Z_ para ponerla en segundo plano (volverá a aparecer la sesión de tu máquina).

Acto seguido introduciremos:

```
stty raw -echo; fg
reset xterm
```

Tras esto retornaremos a la sesión de Netcat, por lo que al introducir _reset_ se reconfigurará de nuevo y nos preguntará el tipo de terminal qué queremos (podría darse algún caso que no pregunte nada). Se puede poner a secas _xterm_, _xterm-256color_ es para formato colorizado.

Solo nos falta exportar las variables de entorno:

```
export TERM=xterm
export SHELL=bash
```

Con esto conseguimos tener los atajos de teclado disponibles como Ctrl+L, y que la _shell_ sea una bash.

> Ahora ya tenemos una TTY totalmente interactiva y que no se nos va a romper, podemos pulsar Ctrl+C sin miedo y tabular para completar comandos.

Podemos realizar un ajuste opcional que nos dará mayor comodidad y en muchos casos es imprescindible también, que es ajustar las filas y columnas de la terminal (si abrimos un editor o introducimos comandos largos veremos que se cortan).

Ahora abriremos una consola en nuestra máquina e introduciremos el siguiente comando:

`stty size`

Este nos dará el número de filas y columnas respectivamente, por lo que solo queda ajustarlas en la sesión de Netcat (en mi caso con estas proporciones):

`stty rows 44 columns 185`

Finalmente, con este resultado tendremos una sesión como si fuese una conexión SSH.
