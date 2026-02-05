# 📝Filezilla: Pruebas con clientes en línea de comandos

## 1. Comprobar que el servidor está activo
En primer lugar vamos a comprobar que el servidor esta activo mediante `sudo systemctl status vsftpd`  .

Nos deberá aparecer `active (runing)`  .


## 2. Instalación de los clientes necesarios
Ubuntu normalmente trae `ftp`, pero vamos a instalar todo por si acaso:  `sudo apt install ftp lftp curl`.  


## 3. Prepararación de archivos de prueba
Creamos un archivo para subir al servidor: `echo "Prueba FTP CLI" > prueba.txt`  .

Con esto, ya tendremos algo que subir al servidor.


## 4. Pruebas
  * ### **Parte A- CLiente ftp(básico)**    
    En primer lugar nos conectamos al servidor: `ftp 10.0.2.15`  .
    
    ![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img1_actividadPruebas.png)

    Una vez hemos hecho login, vamos a ejecutar las siguientes intrucciones:
      * Listar archivos : `ls`  
      * Subir: `put prueba.txt`
      * Descargar: `get prueba.txt`
      * Salir: `exit`

    ![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img2_actividadPruebas.png)

  * ### **Parte B- CLiente lftp**
    En primer lugar nos conectamos al servidor: `lftp usuario1@10.0.2.15`  .

    Una vez hemos hecho login, vamos a ejecutar las siguientes intrucciones:
      * Listar archivos : `ls`  
      * Subir: `put prueba.txt`
      * Descargar: `get prueba.txt`
      * Salir: `exit`

    ![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img3_actividadPruebas.png)

  * ### **Parte C- CLiente curl**
    Vamos a ejecutar las siguientes intrucciones:
      * Listar archivos : `curl -u usuario1 ftp://10.0.2.15/`  
      * Subir: `curl -u usuario1 -T prueba.txt ftp://10.0.2.15/`
      * Descargar: `curl -u usuario1 -O ftp://10.0.2.15/prueba.txt`

    ![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img4_actividadPruebas.png)
    

## 5. Conclusión
Se realizaron pruebas con el cliente curl conectándose mediante autenticación FTP. 
Inicialmente se obtuvo el error 530 (Access denied) debido a credenciales incorrectas. 
Tras usar la opción -u usuario e introducir la contraseña correcta, fue posible listar archivos, subir y descargar ficheros 
correctamente desde la línea de comandos.
