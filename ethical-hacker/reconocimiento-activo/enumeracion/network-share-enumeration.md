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

# Network Share Enumeration

Identificar los sistemas de una red que están compartiendo archivos, carpetas e impresoras es útil para crear una superficie de ataque de una red interna. El script Nmap smb-enum-shares utiliza la llamada a procedimiento remoto de Microsoft (MSRPC) para la enumeración de recursos compartidos en red. La sintaxis del script Nmap smb-enum-shares.nse es la siguiente:

```
nmap --script smb-enum-shares.nse -p 445 192.168.1.251
```

Una forma fácil de realizar una enumeración adicional y la toma de huellas dactilares de las aplicaciones y el sistema operativo que se ejecutan en un host es mediante el comando nmap -sC. La opción -sC ejecuta los scripts NSE más comunes en función de los puertos que se encuentran abiertos en el sistema de destino.

```
nmap -sC 192.168.1.251
```

Tambien se puede usar enum4linux para enumerar recursos compartidos , incluidas cuentas de usuario, recursos compartidos y otras configuraciones.

```
enum4linux 192.168.1.251
```

Se puede también utilizar smbclient para enumerar recursos compartidos y otras información desde un sistema que corre SMB.

<pre><code><strong>smbclient -L \\\192.168.88.251
</strong></code></pre>
