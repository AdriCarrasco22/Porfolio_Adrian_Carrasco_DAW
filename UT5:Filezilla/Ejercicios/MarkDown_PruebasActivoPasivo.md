# 📝Filezilla: Pruebas en modo Activo y Pasivo

## 1. Configuración del rango de puertos pasivos
El modo pasivo requiere que el servidor abra un rango de puertos para la transferencia de datos.  
Para ello vamos a editar el siguiente archivo: `sudo nano /etc/vsftpd.conf`.  

En este archivo añadiremos las siguientes instrucciones:  

`pasv_enable=YES`  ->Habilita el modo pasivo

`pasv_min_port=50000`  

`pasv_max_port=51000`  

Las otras dos instrucciones definen el rango de puertos que usará el servidor para transferir datos.  


## 2. Pruebas de conexión
  * Conexión en modo activo
    `ftp 10.0.2.15`

El FTP por defecto intentará modo activo donde el servidor se conecta al cliente para el canal de datos. Esto requiere que el firewall del cliente permita conexiones entrantes.  

Si quisieramos descargar el archivo que hemos creado en practicas anteriores nos dejaría.  


* Conexión en modo pasivo
  `passive`

  Una vez que hayamos cambiado al modo pasivo volveremos a conectarnos `ftp 10.0.2.15`.

  Si ahora probamos a descaragar el mismo archivo que antes veremos que el cliente abre la conexión al servidor en el puerto   pasivo (50000-51000).

  Funciona mejor con firewalls y NAT porque todas las conexiones son iniciadas por el cliente.


## 3. Tabla comparativa modo activo y pasivo

| Modo       | Cómo funciona                                                   | Ventajas                                                   | Desventajas                                                 |
| ---------- | --------------------------------------------------------------- | ---------------------------------------------------------- | ----------------------------------------------------------- |
| **Activo** | El servidor abre conexión al cliente para enviar datos          | Simplicidad en redes sin firewall                          | Falla si el cliente tiene firewall/NAT                      |
| **Pasivo** | El cliente abre la conexión hacia el puerto pasivo del servidor | Funciona detrás de firewalls y NAT; más seguro en Internet | Requiere configurar rango de puertos pasivos en el servidor |


Como conclusión podemos decir que en redes con firewall o NAT, modo pasivo siempre funciona mejor. 

El modo activo solo es recomendable en redes internas sin restricciones.  

| Característica | Modo Activo | Modo Pasivo |
|---------------|------------|-------------|
| Inicio del canal de control | El cliente inicia la conexión al puerto 21 del servidor | El cliente inicia la conexión al puerto 21 del servidor |
| Canal de datos | El servidor inicia la conexión hacia el cliente | El cliente inicia la conexión hacia el servidor |
| Puertos utilizados | Puerto 21 (control) y puerto 20 (datos) | Puerto 21 (control) y rango de puertos pasivos |
| Configuración en el servidor | No requiere configuración adicional | Requiere definir un rango de puertos pasivos |
| Funcionamiento con firewall | Puede fallar si el cliente tiene firewall o NAT | Funciona correctamente con firewall y NAT |
| Seguridad | Menor, al permitir conexiones entrantes al cliente | Mayor, ya que todas las conexiones las inicia el cliente |
| Uso recomendado | Redes internas sin restricciones | Redes modernas y entornos con seguridad |

