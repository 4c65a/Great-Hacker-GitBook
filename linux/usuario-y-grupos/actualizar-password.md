# Actualizar password

### Actualización de contraseñas de usuario

El comando `passwd` se utiliza para actualizar la contraseña de un usuario. Los usuarios solo pueden cambiar sus propias contraseñas, mientras que el usuario root puede actualizar la contraseña para cualquier usuario.

```
passwd [OPCIONES] [USUARIO]
```

Ejecute el comando `passwd`. Se le pedirá que introduzca la contraseña actual una vez y la contraseña nueva dos veces. Por razones de seguridad, no se muestra ningún resultado mientras se está escribiendo la contraseña. La salida se muestra de la siguiente manera:

<pre><code><strong>sysadmin@localhost:~$ passwd                                                    
</strong>Changing password for sysadmin.                                                 
(current) UNIX password: netlab123                                                       
Enter new UNIX password:                                                       
Retype new UNIX password:                                                       
passwd: password updated successfully
</code></pre>

Si el usuario desea ver información sobre su contraseña, puede utilizar la opción `-S`:

<pre><code><strong>sysadmin@localhost:~$ passwd -S sysadmin                                        
</strong>sysadmin P 12/20/2017 0 99999 7 -1
</code></pre>

Los campos de salida se explican a continuación:

| Campo                   | Ejemplo      | Significado                                                                                                                                                                      |
| ----------------------- | ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Nombre del usuario      | `sysadmin`   | El nombre del usuario.                                                                                                                                                           |
| Estado de la contraseña | `P`          | <p><code>P</code> indica que es una contraseña utilizable.</p><p><code>L</code> indica que la contraseña está bloqueada.</p><p><code>NP</code> indica que no hay contraseña.</p> |
| Fecha de actualización  | `03/01/2015` | La fecha en la que la contraseña fue actualizada por última vez.                                                                                                                 |
| Mínimo                  | `0`          | El número mínimo de días que deben pasar antes de que el usuario pueda cambiar la contraseña actual.                                                                             |
| Máximo                  | `99999`      | El máximo número de días que restan hasta que expire la contraseña.                                                                                                              |
| Aviso                   | `7`          | El número de días precedentes a la expiración de la contraseña para que el usuario reciba el aviso.                                                                              |
| Inactividad             | `-1`         | El número de días después de la expiración de la contraseña que la cuenta del usuario se mantendrá activa.                                                                       |

**Siga leyendo**

Cambie a la cuenta `root` mediante el siguiente comando:

<pre><code><strong>su root                                                   
</strong></code></pre>

El usuario root puede cambiar la contraseña de cualquier usuario. Si el usuario root desea cambiar la contraseña de `sysadmin`, ejecutará el siguiente comando:

<pre><code><strong>passwd sysadmin                                               
</strong>Enter new UNIX password:                                                        
Retype new UNIX password:                                                       
passwd: password updated successfully
</code></pre>

Salga de la cuenta `root` mediante el comando `exit`:

<pre><code><strong>exit                                                        
</strong></code></pre>
