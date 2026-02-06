# 📝Filezilla: Configuración de FTP seguro (FTPS)

## 1. Instalación de FileZilla Server o vsftpd  

Si no tenemos instalado aún vsftpd, como primer paso vamos a instalarlo:  

`sudo apt update`  

`sudo apt install vsftpd`  


## 2. Generar un Certificado TLS

A continuación, vamos a crear un certificado autofirmado:  

`sudo mkdir /etc/ssl/private/ftp`  

`sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/ftp/vsftpd.key -out /etc/ssl/private/ftp/vsftpd.crt`  

Una vez creado, vamos a asegurar los permisos de este certificado:  

`sudo chmod 600 /etc/ssl/private/ftp/vsftpd.key`  


## 3. Configuración vsftpd para FTPS explícito

Ahora vamos a editar el archivo de configuración:  

`sudo nano /etc/vsftpd.conf`  

Dentro de este archivo, nos tendremos que asegurar de que contenga todas estas instrucciones necesarias:  

  * listen=YES
  * listen_ipv6=NO
  * anonymous_enable=NO
  * local_enable=YES
  * write_enable=YES
  * chroot_local_user=YES
  * ssl_enable=YES
  * allow_anon_ssl=NO
  * force_local_data_ssl=YES
  * force_local_logins_ssl=YES
  * rsa_cert_file=/etc/ssl/private/ftp/vsftpd.crt
  * rsa_private_key_file=/etc/ssl/private/ftp/vsftpd.key
  * ssl_tlsv1=YES
  * ssl_sslv2=NO
  * ssl_sslv3=NO


## 4. Reinicio vsftpd

Una vez realizados todos los cambios, vamos a reiniciar nuestro servicio para que se efectuen correctamente:  

`sudo systemctl restart vsftpd`  

`sudo systemctl status vsftpd`  


## 5. Crear usuario FTP

Vamos a crear un usuario local para pruebas:  

`sudo adduser ftpuser`  

Después, vamos a crear una carpeta para el FTP y le daremos permisos:  

`sudo mkdir -p /home/ftpuser/ftp`  

`sudo chown ftpuser:ftpuser /home/ftpuser/ftp`  


## 6. Conexión desde FileZilla Client

Ábriremos FileZilla Client como hemos hecho en la actividad anterio y configuraremos una nueva conexión:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img1_actividadConfigFTP.png)  

Una vez le hemos dado a conectar nos saldrá algo así por pantalla, lo cual nos indica que la conexión esta cifrada:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img2_actividadConfigFTP.png)  


## 7. Conclusion
He realizado pruebas con FileZilla Client conectándome al servidor FTP seguro (FTPS). 
Configuré una conexión guardada con la IP 10.0.2.15, usuario ftpuser y contraseña. 
La conexión se estableció usando FTP explícito sobre TLS, obligando la transmisión cifrada de los datos. 
La ventana de estado de FileZilla mostró la secuencia de comandos y respuestas del servidor.



