# Trabajos y tareas programados

Windows tiene un comando que los atacantes pueden usar para programar la ejecución automatizada de tareas en una computadora local o remota. Puede utilizar esta funcionalidad para post-explotación y persistencia. Puede aprovechar el Programador de tareas de Windows para evitar el Control de cuentas de usuario (UAC) si el usuario tiene acceso a su interfaz gráfica. Esto es posible porque la opción de seguridad se ejecuta con los privilegios más altos del sistema. Cuando un usuario de Windows crea una nueva tarea, el sistema normalmente no requiere que el usuario se autentique con una cuenta de administrador.

**NOTA** Puede acceder a las tareas programadas de un sistema Windows navegando a **Inicio -> Herramientas administrativas -> Programador de tareas** . Alternativamente, puede presionar la **tecla Windows+R** para abrir el cuadro de diálogo Ejecutar y luego escribir **taskchd.msc** y presionar **Enter** .

Las tareas programadas también se pueden utilizar para robar datos a lo largo del tiempo sin generar alarmas. En Windows, el Programador de tareas se puede aprovechar para programar trabajos que pueden utilizar una cantidad significativa de recursos de CPU y ancho de banda de red. Esto es útil cuando se van a comprimir y transferir archivos grandes a través de una red (especialmente si los configura para que se ejecuten por la noche o durante los fines de semana, cuando no habrá usuarios en el sistema de la víctima).