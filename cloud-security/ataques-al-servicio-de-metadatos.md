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

# Ataques al servicio de metadatos

Tradicionalmente, los desarrolladores de software utilizaban credenciales codificadas para acceder a diferentes servicios, como bases de datos y archivos compartidos en un servidor FTP.&#x20;

Para reducir la exposición a prácticas tan inseguras, los proveedores de la nube (como Amazon Web Services \[AWS]) han implementado _servicios de metadatos_ .&#x20;

Cuando una aplicación requiere acceso a activos específicos, puede consultar el servicio de metadatos para obtener un conjunto de credenciales de acceso temporales. Este conjunto temporal de credenciales se puede utilizar para acceder a servicios como los depósitos de AWS Simple Cloud Storage (S3) y otros recursos. Además, estos servicios de metadatos se utilizan para almacenar los datos del usuario proporcionados al iniciar una nueva máquina virtual (VM), como una instancia de Amazon Elastic Compute Cloud o AWS EC2, y configurar la aplicación durante la creación de instancias.

Si puede acceder a estos recursos, como mínimo, obtendrá un conjunto de credenciales de AWS válidas para interactuar con la API. Los desarrolladores de software suelen incluir información confidencial en los scripts de inicio de los usuarios. Se puede acceder a estos scripts de inicio de usuario a través de un servicio de metadatos y permiten que las instancias AWS EC2 se inicien con ciertas configuraciones. A veces, los scripts de inicio incluso contienen nombres de usuario y contraseñas que se utilizan para acceder a diversos servicios.

<mark style="color:red;">**Recursos**</mark>

{% embed url="https://www.sans.org/blog/cloud-instance-metadata-services-imds-/" %}
