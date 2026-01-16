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

## 2. Restringir el acceso al Manager (opcional)







