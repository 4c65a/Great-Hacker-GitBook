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

# Carpetas

**/**: Es el directorio de nivel superior del sistema de archivos. Debe incluir todos los archivos necesarios para arrancar el sistema Linux antes de que se monte otro sistema de archivos. Todos los demás sistemas de archivos se montan en un punto de montaje bien definido y estándar debido a los directorios del sistema de archivos raíz después de que el sistema se inicia.

**/boot**: Incluye el kernel estático y los archivos de configuración y ejecución del gestor de arranque necesarios para iniciar un ordenador Linux.

**/bin**: Este directorio incluye archivos ejecutables de usuario.

**/dev**: Incluye el archivo de dispositivo para todos los dispositivos de hardware conectados al sistema. Estos no son controladores de dispositivos, sino que son archivos que indican todos los dispositivos del sistema y proporcionan acceso a estos dispositivos.

**/etc**: Incluye los archivos de configuración del sistema local para el sistema host.

**/lib**: Incluye archivos de biblioteca compartida que son necesarios para iniciar el sistema.

**/home**: El almacenamiento del directorio de inicio está disponible para los archivos de usuario. Todos los usuarios tienen un subdirectorio dentro de /home.

**/mnt**: Es un punto de montaje temporal para sistemas de archivos básicos que pueden utilizarse en el momento en que el administrador está trabajando o reparando un sistema de archivos.

**/media**: Un lugar para montar dispositivos de medios extraíbles externos, como unidades de memoria USB, que pueden estar vinculados al host.

**/opt**: Contiene archivos opcionales, como programas de aplicación suministrados por el proveedor, que deben colocarse aquí.

**/root**: Es el directorio de inicio del usuario root. Ten en cuenta que no es el sistema de archivos raíz (`/`).

**/tmp**: Es un directorio temporal utilizado por el sistema operativo y varios programas para almacenar archivos temporales. Además, los usuarios pueden almacenar archivos temporalmente aquí.&#x20;

**/sbin**: Estos son archivos binarios del sistema. Son ejecutables utilizados para la administración del sistema.

**/usr**: Son archivos de solo lectura y compartibles, que incluyen bibliotecas ejecutables y binarios, archivos man y varios tipos de documentación.

**/var**: Aquí se guardan los archivos de datos variables. Puede contener cosas como MySQL, archivos de registro, otros archivos de base de datos, bandejas de entrada de correo electrónico, archivos de datos del servidor web y mucho más.
