# Detectar redes de wifi ocultas(hidden) ESSIDs

**Active el modo monitor en su interfaz inalámbrica.**

```
sudo iwconfig wlan0 mode monitor
```

**Escanee las redes inalámbricas cercanas con `airodump-ng`.**

```
airodump-ng -w airodump-ng.cap wlan0mon
```

**Los resultados del escaneo se mostrarán en la terminal.**&#x20;

Las redes ocultas aparecerán como `(ESSID)length`. El `length` es la longitud del SSID de la red oculta.

**Capturando el SSID de una red oculta**

Para capturar el SSID de una red oculta, podemos utilizar la herramienta `aireplay-ng`. Esta herramienta nos permite capturar paquetes de control inalámbricos, incluyendo los paquetes de Beacon. Los paquetes de Beacon son enviados por los puntos de acceso para anunciar su presencia.

Para capturar el SSID de una red oculta con `aireplay-ng`, podemos utilizar el comando `aireplay-ng -0 3 -e MAC -c BSSID wlan0mon`. Este comando realiza un ataque de desautenticación contra el cliente inalámbrico conectado a la red oculta. El ataque de desautenticación provocará que el cliente inalámbrico se desconecte de la red.

Una vez que el cliente inalámbrico se haya desconectado de la red, podemos capturar el paquete de Beacon enviado por el punto de acceso. Este paquete contendrá el SSID de la red oculta.

Por ejemplo, para capturar el SSID de la red oculta con el SSID `SSID_OCULTO` y el BSSID `00:11:22:33:44:55`, podemos ejecutar el siguiente comando:

```
airplay-ng -0 3 -e MAC -c BSSID wlan0mon
```
