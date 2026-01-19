# 📝Tomcat: Configuración de seguridad en Tomcat
## 1. Definir roles y usuarios en `tomcat-users.xml`
 - Primero debemos abrir el archivo `tomcat-users.xml` con el siguiente comando:   

  `sudo nano /etc/tomcat10/tomcat-users.xml`.  

- Después añadimos dentro de `<tomcat-users>` lo siguiente:  
`<role rolename="manager-gui"/>`
`<role rolename="admin-gui"/>`
`<user username="admin" password="Admin123" roles="manager-gui,admin-gui"/>`
`<user username="manager" password="Manager123" roles="manager-gui"/>`

- Por ultimo, reiniciamos TomCat para aplicar cambios:  
  `sudo systemctl restart tomcat10`

## 2. Restringir el acceso al Manager
A continuación, vamos a limitar el acceso por IP.  
- Primero vamos a editar el archivo de contexto del Manager:
  `sudo nano /etc/tomcat10/Catalina/localhost/manager.xml`
  
 Vamos a añadir un filtro por IP para restringir a localhost:
`<Context antiResourceLocking="false" privileged="true">
    <Valve className="org.apache.catalina.valves.RemoteAddrValve"
           allow="127\.0\.0\.1"/>
</Context>
`  
![img](imagen1)

- Posteriormente vamos a reiniciar Tomcat para efectuar los cambios:  
  `sudo systemctl restart tomcat10`
  
## 3. Configurar HTTPS con un keystore
En este paso vamosma asegurar que el acceso sea cifrado con SSL.  

### 3.1 Crear un KEYSTORE:
Ejecutaremos el siguiente comando:  
  `sudo keytool -genkey -alias tomcat -keyalg RSA -keystore /etc/tomcat10/tomcat.jks -keysize 2048`  
 
Después vamos a completar todos los datos solicitados:  
  ![img](imagen2)

### 3.2 Configurar SSL en Tomcat
-Abrimos el archivo `server.xml`:  
`sudo nano /etc/tomcat10/server.xml`  
- Una vez dentro, añadiremos este conector dentro de `<Service name="Catalina">`:  
  ![img](imagen3)
  
 - Por ultimo, reiniciarews Tomcat para ejecutar los cambios:  
`sudo systemctl restart tomcat10`

## 4. Activamos Security Manager
Nuestro objetivo en este apartado de la actividad es limitar permisos del servidor por seguridad:   
`sudo nano /etc/default/tomcat10`  
- Primero vuscaremos la línea con `JAVA_OPTS` y vamos a añadir al final lo siguiente:
  `-Djava.security.manager -Djava.security.policy==/etc/tomcat10/catalina.policy`
- Por ultimo reiniciaremos Tomcat para fecturar los cambios.  
De esta forma estamos activando restricciones adicionales de seguridad.

## 5. Probar el acceso autenticado
Como último paso, vamos a proceder a abir el navegador y vamos a intentar acceder tanto a nuestro Admin como a Manager:  
![img](imagen4)  
![img](imagen5)  

Como vemos hemos podido acceder correctamente al Admin. Ahora vamos a intentar entrar al Manager:  
![img](imagen6)  
![img](imagen7)






  

  


 
  







