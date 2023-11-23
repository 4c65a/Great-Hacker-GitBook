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

# Escaneo post-explotación

El movimiento lateral implica escanear una red en busca de otros sistemas, explotar vulnerabilidades en otros sistemas, comprometer credenciales y recopilar información confidencial para su filtración. El movimiento lateral es posible si una organización no segmenta su red adecuadamente. _Por tanto, la segmentación de la red_ es muy importante.

**NOTA** Es muy importante probar la efectividad de su estrategia de segmentación de red. Es posible que su organización haya implementado firewalls virtuales o físicos, redes de área local virtuales (VLAN) o políticas de control de acceso para la segmentación, o podría utilizar microsegmentación en entornos virtualizados y en contenedores. Debe realizar pruebas de segmentación de red con frecuencia para verificar que su estrategia de segmentación sea adecuada para proteger su red contra movimientos laterales y otros ataques posteriores a la explotación.

Después de comprometer un sistema, puede utilizar escaneos de puertos básicos para identificar sistemas o servicios de interés que puede atacar aún más en un intento de comprometer información valiosa (consulte la Figura 8-5).

En el Módulo 3, “Recopilación de información e identificación de vulnerabilidades”, aprendió sobre las herramientas de escaneo que se utilizan para el reconocimiento activo. Puede utilizar algunas de las mismas herramientas (como Nmap) para realizar el escaneo después de la explotación, y es posible que también desee crear una propia. Alternativamente, existen muchas herramientas, como Metasploit, que tienen capacidades de escaneo integradas para la post-explotación (a través de Meterpreter).



**SUGERENCIA** Un atacante debe evitar generar alarmas en esta etapa. Si los defensores de la seguridad detectan que hay una amenaza en la red, la examinarán minuciosamente y frustrarán cualquier progreso que haya logrado. En algunos casos de pruebas de penetración, puede comenzar de manera muy sigilosa y aumentar gradualmente la cantidad de tráfico y herramientas automatizadas utilizadas para probar también la efectividad de los defensores de la seguridad (incluido el centro de operaciones de seguridad \[SOC]).
