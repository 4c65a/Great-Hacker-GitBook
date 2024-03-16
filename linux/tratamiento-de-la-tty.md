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

1. `script /dev/null -c bash`
2. `python3 -c 'import pty;pty.spawn("/bin/bash")'`

Una vez hemos ejecutado una de estas “consolas”, debemos pulsar _Ctrl+Z_ para ponerla en segundo plano (volverá a aparecer la sesión de tu máquina).

Acto seguido introduciremos:

```
stty raw -echo; fg
reset xterm
```

Tras esto retornaremos a la sesión de Netcat, por lo que al introducir _reset_ se reconfigurará de nuevo.Se puede poner a secas _xterm_, _xterm-256color_ es para formato colorizado.

Solo nos falta exportar las variables de entorno:

```
export TERM=xterm
export SHELL=bash
```

Con esto conseguimos tener los atajos de teclado disponibles como Ctrl+L, y que la _shell_ sea una bash.

Ahora abriremos una consola en nuestra máquina e introduciremos el siguiente comando:

`stty size`

Este nos dará el número de filas y columnas respectivamente, por lo que solo queda ajustarlas en la sesión de Netcat.

`stty rows 44 columns 185`

