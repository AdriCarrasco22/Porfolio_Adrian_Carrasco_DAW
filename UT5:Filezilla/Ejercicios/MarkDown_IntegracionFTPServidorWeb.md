
# 📝Filezilla: Integración de FTP con servidor web

## 1. Instalar Apache si aún no lo hemos hecho

En primer lugar nos vamos a asegurar de tener un servidor web funcionando:  

`sudo apt update`  

`sudo apt install apache2 -y`  

Ahora verificaremos que abriendo en nuestro navegador: `http://10.0.2.15` deberíamos ver la página por defecto de Apache.


## 2. Vincular el directorio FTP con el DocumentRoot

El "DocumentRoot" de Apache es `/var/www/html`. Vamos a hacer que el directorio de nuestro `ftpuser` apunte ahí para que lo que subamos por FTP se publique automáticamente en la web.

En primer lugar vamos a cambiar el directorio home del usuario:  

`sudo usermod -d /var/www/html ftpuser`  

Después, vamos a ajustar permisos de propiedad para que el usuario FTP pueda escribir y Apache pueda leer:  

`sudo chown -R ftpuser:www-data /var/www/html`  

`sudo chmod -R 775 /var/www/html`  

Por útlimo, vamos a añadir a ftpuser al grupo de la web:  

`sudo usermod -a -G www-data ftpuser`  


## 3. Subir contenido vía FTP

Ahora vamos a abrir FileZilla y nos vamos a conectar a nuestra IP.

Hemos creado un archivo de prueba .html básico para que se nuos muestre una bienvenida al abrirlo.

Ahora, una vez estamos dentro de Filezilla vamos a subir el archivo que hemos creado: 

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img1_actividadIntegracionFTP.png)  


## 4. Comprobación via HTTP

Ahora vamos a comprobar que nuestra red local puede ver lo que acabamos de subir.

Vamos a utilizar la siguiente dirección en nuestro navegador: 

`https://miweb.local/practica10.html`  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img2_actividadIntegracionFTP.png)  


## 5. Conclusión

Con esta actividad hemos demostrado con éxito la automatización del flujo de publicación web mediante la sincronización de servicios. Al vincular el directorio raíz de Apache (/var/www/html) con el acceso del servidor FTP, se ha logrado un entorno de despliegue profesional donde:

  *  **Eficiencia:** Nosotros como desarrolladores podemos subir actualizaciones de forma remota y segura sin necesidad de          acceder a la consola del servidor.
    
  *  **Disponibilidad inmediata:** El servidor web sirve el contenido en tiempo real en cuanto la transferencia FTP                 finaliza, optimizando los tiempos de puesta en producción.
    
  *  **Separación de protocolos:** Se utiliza FTPS (puerto 21) para la gestión y administración de archivos, mientras se            reserva HTTP (puerto 80) para la consulta pública de los usuarios finales.

