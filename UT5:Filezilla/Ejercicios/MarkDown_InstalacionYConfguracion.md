# 📝Filezilla: Instalación y configuración inicial del servidor

## 1. Instalar el servidor FTP (vsftpd)
En primer lugar vamos a instalar el servicio FTP mediante:
`sudo apt install vsftpd`  


## 2. Comprobación de que el servicio está funcionando
Para comprobar que lo hemos instalado correctamente y que esta funcionando, ejecutaremos el siguiente comando:  
`sudo systemctl status vsftpd`   

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img1_actividadInstal.png)  


Como podemos ver, nos aparece como que nuestro servidor ha cargado y que por tanto esta activo (running)


## 3. Acceder a la “consola de administración”
Como en nuestra Máquina Virtual manejamos Linux, la administración del servidor FTP se hace mediante archivo de configuración y no con una interfaz gráfica.  

El archivo principal al que nos dirijiremos será:
`sudo nano /etc/vsftpd.conf`  


## 4. Configurar el puerto de escucha
Por defecto, FTP usa el puerto 21 por lo que solo tendremos que verificar si en nuestro archivo de configuración así esta establecido.


## 5. Configurar la dirección IP
Por defecto, el servidor escucha en todas las interfaces.  

Para comprobar la IP de nuestro UIbuntu vamos a ejecutar: `ip a`  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img2_actividadInstal.png)  

En esta imagen podemos comprobar la IP la cual necesitaremos para el cliente FTP.


## 6. Configurar el inicio automático del servicio
Ejecutaremos `sudo systemctl enable vsftpd`  para que el servidor FTP se inicie automaticamente al arrancar el sistema.  

Para aplicar los cambios, posteriormente ejecutaremos `sudo systemctl restart vsftpd`  


## 7. Verificar que el puerto está escuchando
A continuación vamos a verificar que el servidor escucha en el puerto 21.  
`sudo ss -tulpn | grep vsftpd`  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img3_actividadInstal.png)  


## 8. Probar que el servidor funciona
Para comprobar que el servidor funciona correctamente ejecutaremos: `ftp IP_DEL_SERVIDOR`  

En nuestro caso, la IP es: `ftp 127.0.0.1`

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img4_actividadInstal.png) 

Como vemos se nos pedirá un usuario y contraseña, lo que nos dice que el servidor esta funcionando.

## 9. Conclusión
En esta práctica he instalado y configurado un servidor FTP en Ubuntu mediante el servicio vsftpd. Tras la instalación, he comprobado que el servicio se encuentra activo y configurado para iniciarse automáticamente con el sistema. También he verificado el puerto de escucha y la dirección IP del servidor, asegurando que acepta conexiones correctamente. Finalmente, he confirmado el funcionamiento del servidor.




