# Falsa autenticación

Al autenticarnos falsamente, podremos inyectar paquetes en la red, generar tráfico y capturar los datos necesarios para descifrar la clave WEP.

Si no hay clientes activos en la red, debes realizar una autenticación falsa para que la red acepte paquetes desde tu tarjeta Wi-Fi. Esto engañará al punto de acceso haciéndole creer que tu dispositivo es un cliente legítimo.

## Pasos de falsa autenticación

Realizar la captura de datos de la red

```
airodump-ng -c 6 --bssid 55:LE:D2:42:23:50 -w crackwep wlan0
```

Inyectar paquetes falsos

```
 aireplay-ng -1 0 -a 55:LE:D2:42:23:50  -h 00:0C:55:78:AC:10 wlan0
```

Una vez que esto ocurra ,aumentara los paquetes capturados con airodump y a partir de eso se podría conseguir la password.
