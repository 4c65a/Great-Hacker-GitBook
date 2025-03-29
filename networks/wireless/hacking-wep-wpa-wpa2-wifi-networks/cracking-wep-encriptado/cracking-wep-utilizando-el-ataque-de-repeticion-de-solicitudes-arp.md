# Cracking WEP utilizando el Ataque de Repetición de Solicitudes ARP

El ataque **ARP Request Replay** se utiliza para capturar y aprovechar las solicitudes ARP (Address Resolution Protocol) para obtener claves de redes Wi-Fi con seguridad WEP. Este ataque se basa en la inyección de paquetes ARP en el tráfico para generar más paquetes con vectores de inicialización (IVs), lo que ayuda a descifrar la clave WEP.

1\. **Seleccionar el objetivo**

Primero, debes seleccionar el objetivo, que es la red que deseas atacar. Utiliza herramientas como `airodump-ng` para identificar el BSSID (la dirección MAC del punto de acceso) y el canal de la red objetivo.

```
airodump-ng --bssid <BSSID> --channel <canal> -w <archivo_salida> <interfaz>
```

#### 2. **Autenticación falsa**

Para poder inyectar paquetes en la red, debes autenticarte en ella. Esto se logra utilizando el comando `aireplay-ng` con la opción `-1` para la autenticación falsa. Este paso permite que tu tarjeta Wi-Fi se "conecte" al punto de acceso y te permita inyectar paquetes en la red.

```bash
aireplay-ng -1 0 -a <BSSID> -h <tu_MAC> <interfaz>
```

#### 3. **Capturar paquetes ARP**

Una vez que te has autenticado, el siguiente paso es capturar un paquete ARP de la red. Los paquetes ARP se utilizan para resolver direcciones IP a direcciones MAC, y son muy útiles para este tipo de ataques.

Utiliza `airodump-ng` para capturar los paquetes ARP:

```bash
airodump-ng --bssid <BSSID> --channel <canal> -w <archivo_salida> <interfaz>
```

#### 4. **Inyectar paquetes ARP**

Luego de haber capturado un paquete ARP, puedes utilizar `aireplay-ng` para inyectar este paquete en la red. Al inyectar el paquete, se generan más paquetes con IVs nuevos, lo que aumenta la cantidad de datos que puedes capturar.

El comando para inyectar el paquete ARP es:

```bash
aireplay-ng -3 -b <BSSID> -h <tu_MAC> <interfaz>
```

* `-3`: Indica que estamos inyectando paquetes ARP en la red.

#### 5. **Repetir la inyección para generar más IVs**

El proceso de inyección se repite para generar más paquetes y conseguir suficientes IVs (vectores de inicialización) para romper la clave WEP. A medida que los paquetes ARP inyectados circulan en la red, aumentará rápidamente el número de IVs capturados, lo que hace más probable que puedas descifrar la clave WEP.

#### 6. **Descifrar la clave**

Una vez que tengas suficientes IVs, puedes usar `aircrack-ng` para intentar descifrar la clave WEP:

```bash
aircrack-ng -b <BSSID> <archivo_salida>.cap
```

Mas informacion:

[https://www.aircrack-ng.org/doku.php?id=es:arp\_amplification](https://www.aircrack-ng.org/doku.php?id=es:arp_amplification)
