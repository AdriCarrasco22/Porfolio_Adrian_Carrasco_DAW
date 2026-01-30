# 📝Filezilla: Creación de usuarios y Grupos

## 1. Creción de grupo con permisos limitados
Primero creamos un grupo específico para los usuarios FTP mediante `sudo groupadd ftp_limitado`.  

En este grupo agruparemos usuarios FTP y controlaremos permisos de forma conjunta.

## 2. Creación del directorio raíz para el FTP
A continuación crearemos un directorio que será el directorio raíz común del gurpo:  
`sudo mkdir -p /srv/ftp/limitado`.  

Después, vamos a asignar el grupo como propietario mediante `sudo chown root:ftp_limitado /srv/ftp/limitado` y vamos a dar alguno permisos limitados `sudo chmod 750 /srv/ftp/limitado`.  

Estos permisos significan:
  * **Propietario (root):** lectura, escritura y ejecución
  * **Grupo (ftp_limitado):** lectura y ejecución
  * **Otros:** sin acceso

## 3. Creación de los usuarios asociados al grupo
Vamos a crear dos usuarios para realizar esta actividad.  
  * Usuario 1  
    `sudo useradd -m -G ftp_limitado -d /srv/ftp/limitado usuario1`  
    `sudo passwd usuario1`
  Contraseña: qwerty$2001

  * Usuario 2
    `sudo useradd -m -G ftp_limitado -d /srv/ftp/limitado usuario2`
    `sudo passwd usuario2`
    Contraseña: qwerty$2002  

Ambos usuarios pertenecen al grupo `ftp_limitado` y comparten el mismo directorio raíz FTP.  


## 4. Configuración de permisos de escritura y borrado
En este apartado, vamos a editar el archivo de configuración de vsftpd.  

Nos aseguraremos de que en nuestro archivo de configuración aparezca lo siguiente:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img1_actividadUsuarios.png)  

Estos permisos nos permitirán: 
  * Subir archivos
  * Borrar archivos
  * Modificar contenido


## 5. Definir el directorio raíz (chroot)
Para que los usuarios no puedan salir de su carpeta FTP comprobaremos que en nuestro archivo de configuración aparece lo siguiente:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img2_actividadUsuarios.png)  

Esto encierra a los usuarios en su directorio raíz y evita accesos al resto del sistema.  


## 6. Configuración de límites de conexión
Posteriormente, vamos a establecer un limite de conexión en el que máximo se permitan 10 conexiones simultaneas al servidor y máximo haya 2 conexiones por IP.  

`max_clients=10`  `max_per_ip=2`  


## 7. Comprobaciones necesarias
En primer lugar vamos a verificar usuarios y grupo: `getent group ftp_limitado`.  

En segundo lugar vamos a hacer una prueba de conexión FTP: `ftp 10.0.2.15`.  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img3_actividadUsuarios.png)  

Como podemos ver, tenemos nuestro grupo `ftp_limitado` creado y dos usuarios asignados, además de comprobar que la conexión FTP `ftp 10.0.2.15` funciona. 


## 8. Diferencias entre permisos de usuario y permisos de grupo

Los `permisos de usuario` se aplican de forma individual y determinan las acciones que un usuario concreto puede realizar sobre un archivo o directorio, como leer, escribir o borrar contenido. Estos permisos permiten un control específico y personalizado para cada cuenta.

Los `permisos de grupo`, en cambio, se aplican de manera conjunta a todos los usuarios que pertenecen a un mismo grupo. Esto facilita la administración, ya que permite asignar permisos comunes a varios usuarios sin necesidad de configurarlos uno por uno. En un servidor FTP, el uso de grupos resulta especialmente útil para gestionar accesos y limitar privilegios de forma centralizada.  






