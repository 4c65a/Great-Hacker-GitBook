---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Resolución de nombres de Windows

Existen varias tecnologías y protocolos de resolución de nombre a dirección IP, incluido el sistema básico de entrada/salida de red (NetBIOS), la resolución de nombres de multidifusión local de enlace (LLMNR) y el sistema de nombres de dominio (DNS).

## **Servicio de nombres NetBIOS y LLMNR**

NetBIOS y LLMNR son protocolos que Microsoft Windows utiliza principalmente para la identificación del host. LLMNR, que se basa en el formato del protocolo DNS, permite a los hosts en el mismo enlace local realizar la resolución de nombres para otros hosts. Por ejemplo, un host de Windows que intenta comunicarse con una impresora o una carpeta compartida de red puede usar NetBIOS

NetBIOS proporciona tres servicios diferentes:

* Servicio de nombres NetBIOS (**NetBIOS-NS**) para registro y resolución de nombres
* Servicio de datagramas (**NetBIOS-DGM**) para comunicación sin conexión
* Servicio de sesión (**NetBIOS-SSN**) para comunicación orientada a la conexión

Las operaciones relacionadas con NetBIOS utilizan los siguientes puertos y protocolos:

* **Puerto TCP 135:** asignador de puntos finales de llamada a procedimiento remoto de Microsoft (MS-RPC), utilizado para la comunicación de cliente a cliente y de servidor a cliente
* **Puerto UDP 137:** Servicio de nombres NetBIOS
* **Puerto UDP 138:** Servicio de datagramas NetBIOS
* **Puerto TCP 139:** Servicio de sesión NetBIOS
* **Puerto TCP 445:** protocolo SMB, utilizado para compartir archivos entre diferentes sistemas operativos, incluidos Windows y sistemas basados ​​en Unix.

La vulnerabilidad en LLMNR permite a un atacante suplantar una fuente de resolución de nombres autorizada al responder al tráfico LLMNR a través de los puertos UDP 5355 y 137. Al envenenar el servicio LLMNR, el atacante manipula el sistema de la víctima, obteniendo potencialmente nombres de usuario y hashes NTLMv2. Estos datos pueden ser recopilados a través de la red y luego utilizados para realizar ataques de fuerza bruta o descifrar contraseñas fuera de línea.

Herramientas como NBNSpoof, Metasploit y Responder se pueden utilizar para llevar a cabo este tipo de ataques. Metasploit es especialmente conocido y utilizado en entornos de evaluación de penetración. Además, Pupy, una herramienta de administración remota basada en Python, también puede utilizarse con fines maliciosos.

Para mitigar estos ataques, se recomienda deshabilitar LLMNR y NetBIOS en la configuración de seguridad de la computadora local o mediante políticas de grupo. También se sugiere establecer políticas de control de acceso adicionales para bloquear el tráfico LLMNR/NetBIOS si no son necesarios. Una técnica común de detección implica monitorear la clave de registro `HKLM\Software\Policies\Microsoft\Windows NT\DNSClient` para cambios en el valor DWORD `EnableMulticast`. Un valor de cero indica que LLMNR está deshabilitado.

### Explotación SMB&#x20;

Uno de los exploits para `smb` más utilizados en los últimos tiempos ha sido el exploit EternalBlue.La explotación exitosa de EternalBlue permite que un atacante remoto no autenticado comprometa un sistema afectado y ejecute código arbitrario. Este exploit se ha utilizado en ransomware cómo WannaCry y Nyeta. Este exploit se ha adaptado a muchas herramientas diferentes, incluido Metasploit.

```
msf> usar exploit/windows/smb/ms17_010_eternalblue
```

