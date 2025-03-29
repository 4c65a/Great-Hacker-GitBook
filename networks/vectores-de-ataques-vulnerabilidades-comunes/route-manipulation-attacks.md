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

# Route Manipulation Attacks

No de los más comunes es el ataque de secuestro de BGP. Border Gateway Protocol (BGP) es un protocolo de enrutamiento dinámico que se utiliza para enrutar el tráfico de Internet. Un atacante puede lanzar un ataque de secuestro de BGP configurando o comprometiendo un enrutador perimetral para anunciar prefijos que no han sido asignados a su organización. Si el anuncio malicioso contiene una ruta más específica que el anuncio legítimo o presenta una ruta más corta, el tráfico de la víctima podría redirigirse al atacante. En el pasado, los actores de amenazas han aprovechado prefijos no utilizados para el secuestro de BGP con el fin de evitar la atención del usuario u organización legítimo.
