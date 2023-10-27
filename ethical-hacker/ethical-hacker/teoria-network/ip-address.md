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

# IP Address

IP se diseñó como un protocolo con sobrecarga baja. Provee solo las funciones necesarias para enviar un paquete de un origen a un destino a través de un sistema interconectado de redes. El protocolo no fue diseñado para rastrear ni administrar el flujo de paquetes. Estas funciones, si es necesario, están a cargo de otros protocolos en otras capas, principalmente TCP en la capa 4.

Estas son las características básicas de la IP:

* **Sin conexión** - no hay conexión con el destino establecido antes de enviar paquetes de datos.
* **Mejor esfuerzo** - la IP es inherentemente poco confiable porque no se garantiza la entrega de paquetes.
* **Medios independientes** - la operación es independiente del medio (es decir, cobre, fibra óptica o inalámbrico) que transporta los datos.
