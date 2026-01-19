# 📝Tomcat: Configuración de seguridad en Tomcat
## 1. Acceder al Manager
`http://localhost:8080/manager/html`  
Se nos pedirán las credenciales de Usuario y contraseña como hemos visto en la practica anterior (User: manager; Pass: Manager123).

Una vez hayamos accedido, nos aparecerá lo siguiente:  
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img1_actividadHerramientas.png)  

## 2. Pruebas controladas en `Manager`
## 2.1 Prueba de recarga(Reload)
Como primera prueba nos dirigiremos a la app `/sample` y haremos click en **RECARGAR**.    

Como resultado vamos a ver que la página se nos recarga sin error alguno. 

Esto nos quiere decir que la recarga reinicia la aplicación sin detener el servidor.  

## 2.1 Prueba de parada y arranque
Como segunda prueba nos dirigiremos a la misma app `/sample` y haremos click en **PARAR** .  

Si ahora queremos acceder a `http://localhost:8080/sample` nos aparecerá **ERROR 404**.  

Esto nos quiere decir que no se ha encontrado la página ya que la hemos parado.  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img2_actividadHerramientas.png)  

Si volvemos a **ARRANCAR** la aplicacion `/sample` veremos que si que podrémos acceder a su página:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img3_actividadHerramientas.png)  

## 3. Acceder a Host Manager
En la misma ventana introduciremos las credenciales del usuario con rol `admin-gui` (User: admin; Pass:Admin123).  

Se nos abrirá de nuevo una ventana como la que hemos podido ver cuando hemos accedido con **Manager** en la cual también vamos a encontrar las diferentes herramientas como `Parar, Recargar, Replegar...`.  

## 4. Fichas descriptivas
  ## 2.1 Ficha **Manager**
  
*Nombre*: Tomcat Manager  
*Función*: Gestión de aplicaciones web  
*Acceso*: Usuario con rol manager-gui  

#### **Funciones principales:**

- Despliegue de aplicaciones WAR

- Arranque y parada de aplicaciones

- Recarga sin reiniciar el servidor

- Eliminación de aplicaciones

- Visualización de información del servidor
  
- Uso típico: Administración del ciclo de vida de aplicaciones web.

## 2.2 Ficha **Host Manager**
  
*Nombre*: Tomcat Host Manager  
*Función*: Gestión de hosts virtuales  
*Acceso*: Usuario con rol admin-gui  

#### **Funciones principales:**

- Creación de hosts virtuales

- Configuración de dominios y alias

- Gestión del despliegue por host
  
- Uso típico: Alojar múltiples dominios en un mismo servidor Tomcat.







