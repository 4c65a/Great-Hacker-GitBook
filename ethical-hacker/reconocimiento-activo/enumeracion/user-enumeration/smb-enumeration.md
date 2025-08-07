# SMB enumeration

Recopilar una lista  de usuarios. Cuando tienes el nombre de usuario, puedes comenzar a realizar intentos de fuerza bruta para obtener la contraseña de la cuenta. Realizas la enumeración de usuarios cuando has obtenido acceso a la red interna.

En una red Windows, puedes hacer esto manipulando el protocolo Server Message Block (SMB).

El script smb-enum-users.nse es un script Nmap que se utiliza para enumerar usuarios en sistemas Windows. El script funciona enviando mensajes SMB especialmente diseñados al servidor SMB. Si el servidor SMB es vulnerable, responderá con una lista de usuarios.

```
nmap  --script smb-enum-users.nse 192.168.88.251
```

