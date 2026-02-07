# 📝Filezilla: Disponibilidad y Buenas Prácticas

## 1. Lista de Recomendaciones: Servidor FTP en Producción

  * Límites de Conexión (Garantizar la Disponibilidad):
    
    Para evitar que un solo usuario o un ataque de Denegación de Servicio (DoS) sature el servidor, tenemos que limitar los recursos:

      * **Límites por IP:** Configurar un máximo de conexiones simultáneas desde la misma dirección IP (por ejemplo, 3 o 5).

      * **Límites de ancho de banda:** Establecer un máximo de velocidad de transferencia (local_max_rate en vsftpd) para que el tráfico FTP no sature la red del servidor web.

      * **Tiempo de espera (Timeout):** Configurar el cierre automático de sesiones inactivas para liberar puertos y memoria.

---
  * Logs y Auditoría (Trazabilidad):
    
    Cuando estamos producción, debemos saber quién, cuándo y qué se ha modificado:

      * **Activar el registro detallado:** Debemos asegurarnos de que `xferlog_enable=YES` y `log_ftp_protocol=YES` estén activos en la configuración.

      * **Centralización de Logs:** Enviar los registros a /var/log/vsftpd.log y usar herramientas como `Logrotate` para que los archivos de log no llenen el disco duro.

      * **Auditoría de Errores:** Revisar periódicamente los intentos de acceso fallidos, ya que pueden indicar ataques de fuerza bruta.

---
  * Copias de Seguridad (Integridad de Datos):

    El FTP es una vía de entrada; si algo se borra por error, debe haber un plan B:

      * **Backup del archivo de configuración:** Mantener siempre una copia de `/etc/vsftpd.conf` antes de cualquier cambio.

      * **Copias programadas:** Usar tareas de Cron para realizar copias de seguridad diarias de las carpetas de los usuarios FTP (/var/www/html) en un almacenamiento externo.

      * **Regla 3-2-1:** Mantener 3 copias de los datos, en 2 soportes diferentes y 1 fuera del servidor principal para tener una mayor seguridad.

---
  * Firewall y NAT (Seguridad de Red):

    El servidor no debe estar totalmente expuesto a Internet:

      * **Uso de Puertos Pasivos:** Configurar un rango específico de puertos para el modo pasivo (ej. 50000-51000) y abrirlos exclusivamente en el firewall.

      * **Bloqueo por fuerza bruta:** Instalar y configurar `Fail2Ban`. Esta herramienta banea automáticamente las IPs que intentan entrar con contraseñas erróneas varias veces.

      * **Restricción de puertos:** Cerrar el puerto 21 para todo el mundo excepto para las IPs de confianza, o usar un puerto distinto al 21 para evitar escaneos automáticos de bots.
