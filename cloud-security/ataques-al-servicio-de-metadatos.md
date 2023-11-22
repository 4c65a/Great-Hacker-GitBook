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

Tradicionalmente, los desarrolladores de software utilizaban credenciales codificadas para acceder a diferentes servicios, como bases de datos y archivos compartidos en un servidor FTP. Para reducir la exposición a prácticas tan inseguras, los proveedores de la nube (como Amazon Web Services \[AWS]) han implementado _servicios de metadatos_ . Cuando una aplicación requiere acceso a activos específicos, puede consultar el servicio de metadatos para obtener un conjunto de credenciales de acceso temporales. Este conjunto temporal de credenciales se puede utilizar para acceder a servicios como los depósitos de AWS Simple Cloud Storage (S3) y otros recursos. Además, estos servicios de metadatos se utilizan para almacenar los datos del usuario proporcionados al iniciar una nueva máquina virtual (VM), como una instancia de Amazon Elastic Compute Cloud o AWS EC2, y configurar la aplicación durante la creación de instancias.

Como probablemente ya podrá adivinar, los servicios de metadatos son algunos de los servicios más atractivos de AWS al que puede acceder un atacante. Si puede acceder a estos recursos, como mínimo, obtendrá un conjunto de credenciales de AWS válidas para interactuar con la API. Los desarrolladores de software suelen incluir información confidencial en los scripts de inicio de los usuarios. Se puede acceder a estos scripts de inicio de usuario a través de un servicio de metadatos y permiten que las instancias AWS EC2 (o servicios similares con otros proveedores de la nube) se inicien con ciertas configuraciones. A veces, los scripts de inicio incluso contienen nombres de usuario y contraseñas que se utilizan para acceder a diversos servicios.

Al utilizar herramientas como nimbostratus [_(https://github.com/andresriancho/nimbostratus_](https://github.com/andresriancho/nimbostratus) ), puede encontrar vulnerabilidades que podrían provocar _**ataques al servicio de metadatos**_ .

![](https://skillsforall.com/content/eh/1.0/m7/course/en-US/assets/e9925ad4fdb51201d6364cb313b5aa2265c84d84.png)

**SUGERENCIA** Cuando esté realizando una prueba de penetración de una aplicación web, busque una funcionalidad que obtenga datos de la página y los devuelva al usuario final (de forma similar a como lo haría un proxy). El servicio de metadatos no requiere ningún parámetro particular. Si accede a la URL https://xxxx/latest/meta-data/iam/security-credentials/IAM\_USER\_ROLE\_HERE, devolverá los valores AccessKeyID, SecretAccessKey y Token que necesita para autenticarse en la cuenta.
