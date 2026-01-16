# 📝Integración de Tomcat + Servidor Web

## 1. Habilitar módulos de proxy y proxy_http
Para habilitar los módulos de proxy y proxy_http utilizaremos los siguientes comandos:
* `sudo a2enmod proxy`
* `sudo a2enmod proxy_http`
* `sudo systemctl restart apache2` (para efectuar los comandos ejecutados anteriormente)

## 2. Configuración del Conector (Reverse Proxy)
Para la configuración, configuraremos un proxy inverso sobre HTTP, que es el estándar actual por su facilidad de depuración. 

En primer lugar vamos a crear el archivo de configuración mediante `sudo nano /etc/apache2/sites-available/tomcat-proxy.conf`. 

En segundo lugar, vamos a añadir las reglas de redirección:

    ServerName localhost

    ProxyPreserveHost On

    # Redirigir el tráfico de la raíz a la aplicación 'sample' en Tomcat
    ProxyPass /sample http://127.0.0.1:8080/sample
    ProxyPassReverse /sample http://127.0.0.1:8080/sample

    ErrorLog ${APACHE_LOG_DIR}/tomcat_proxy_error.log
    CustomLog ${APACHE_LOG_DIR}/tomcat_proxy_access.log combined

Después, vamos a habilitar el sitio y a reiniciar Apache para que se efectuen todos los cambios mediante los siguientes comandos:  
* `sudo a2ensite tomcat-proxy.conf`
* `sudo a2dissite 000-default.conf` (Este comando desactiva el sitio por defecto para evitar conflictos)
* `sudo systemctl restart apache2`

## 4. Verificación
Para verificar que hemos realizado la práctica correctamente, debemos acceder sin especificar el puerto 8080, ya que Apache está haciendo el puente:  `http://localhost/sample`.

Como resultado encontraremos: 
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img1_actividad4.png)




