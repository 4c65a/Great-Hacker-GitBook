# Demonios personalizados, procesos y puertas traseras adicionales

Al igual que con las tareas programadas, puede crear sus propios demonios (servicios) y procesos personalizados en un sistema víctima, así como puertas traseras adicionales. Siempre que sea posible, una puerta trasera debe sobrevivir a los reinicios para mantener la persistencia en el sistema de la víctima. Puede garantizar esto creando demonios que se inicien automáticamente durante el arranque. Estos demonios pueden persistir en el sistema para comprometer aún más otros sistemas (movimiento lateral) o filtrar datos.
