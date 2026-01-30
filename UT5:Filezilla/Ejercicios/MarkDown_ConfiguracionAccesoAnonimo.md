# 📝Filezilla: Configuración de Acceso Anónimo

## 1. ¿Qué es el acceso anónimo en FTP?
El acceso anónimo permite que cualquier cliente FTP se conecte al servidor sin usuario ni contraseña, usando el usuario anonymous o ftp.
Normalmente se usa solo para descarga de archivos, nunca para subir o borrar, por motivos de seguridad.  

## 2. Creación del directorio para el acceso anónimo
En primer lugar vamos a crear un directorio exclusivo para los usuarios anónimos: `sudo mkdir -p /srv/ftp/anonimo`.  

Una vez creado el directorio, vamos a asignarle propietario y grupo:  `sudo chown ftp:ftp /srv/ftp/anonimo`.  

Unicamente le vamos a asignar permisos solo de lectura:  `sudo chmod 555 /srv/ftp/anonimo`.  

El `555` significa:
  * Lectura y ejecucción para todos
  * Sin escritura
  * Impide subir, borrar o modificar archivos


## 3. Añadir archivos de prueba
Vamos a crear a un archivo visible para el usuario anónimo: `sudo nano /srv/ftp/anonimo/README.txt` con un ejemplo de contenido de "Acceso anonimo permitido solo en modo lectura".  

A continuación, aseguraremos los permisos correctos:  `sudo chmod 444 /srv/ftp/anonimo/README.txt`.  


## 4. Configuración de vsftpd para permitir acceso anónimo
Para realizar este paso, necesitaremos editar el archivo de configuración:  `sudo nano /etc/vsftpd.conf` estableciendo las siguientes líneas:  

`anonymous_enable=YES`  
`anon_root=/srv/ftp/anonimo`  
`write_enable=NO`  
`anon_upload_enable=NO`  
`anon_mkdir_write_enable=NO`  
`anon_other_write_enable=NO`  

Esto sifnifica que:
  * Se permite acceso anónimo
  * Se limita el acceso al directorio indicado
  * Se prohíbe cualquier tipo de escritura


## 5. Conexión como usuario anónimo
Desde nuestra máquina ejecutaremos `ftp 10.0.2.15` y veremos todas las instrucciones de prueba que he realizado para ver que todo funciona según lo previsto, entrando sin usuario especificado y con permisos limitados:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img1_actividadAnonymous.png)  

Con esta imagen confirmamos que la lectura del archivo ha sido permitida y que la escritura ha sido denegada ya que no tenemos permisos.  


## 6. Conclusión
En esta práctica he configurado el acceso anónimo al servidor FTP utilizando vsftpd. 
Hemos limitado el acceso a un directorio específico y hemos establecido permisos únicamente de lectura, impidiendo la subida, 
modificación o borrado de archivos.  

La conexión se ha realizado correctamente como usuario anónimo desde un cliente FTP, permitiendo el listado 
y la descarga de archivos, mientras que las operaciones de escritura han sido denegadas, 
confirmando el correcto funcionamiento de la configuración.







