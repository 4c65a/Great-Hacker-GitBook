# Captura de paquetes de un punto de acceso Wi-Fi específico

Para realizar la captura de paquetes específicos se puede utilizar estos comandos:

```
sudo airodump-ng --channel 6 --bssid AA:HH:JJ:12:45:48 --write redSecurity wlan0
```

* **--channel 6:** Especifica que la captura se enfocará únicamente en el canal 6 de la banda Wi-Fi.
* **--bssid AA:HH:JJ:12:45:48:** Filtra la captura para mostrar solo los paquetes relacionados con el punto de acceso con la dirección MAC indicada.
* **--write redSecurity:** Guarda la captura de paquetes en un archivo llamado "redSecurity".
* **wlan0:** Indica la interfaz de red inalámbrica que se utilizará para la captura.

**Tambien se puede especificar el tiempo de captura:** La opción `-t` se puede utilizar para especificar la duración de la captura de paquetes. Por ejemplo, para capturar paquetes durante 10 minutos, se utilizaría el siguiente comando:

```
sudo airodump-ng --channel 6 --bssid AA:HH:JJ:12:45:48 --write redSecurity wlan0 -t 600
```
