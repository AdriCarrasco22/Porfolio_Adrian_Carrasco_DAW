# 📝Practica Tomcat: Investigación y Descripción
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/logoTomcat.png)  
## 1. Elementos de Tomcat: para qué sirven y donde se ubican

### CATALINA

Catalina es como el corazón de Tomcat. Es el jefe que se encarga de que las páginas web hechas con Java funcionen bien.  

Cuando alguien entra a una página, Catalina recibe la petición y se la pasa al programa correcto.También se ocupa de encender y apagar esos programas.

Este elemento se encuentra dentro de la carpeta de Tomcat, en un archivo llamado `server.xml` que está en la carpeta `conf`.

Todo lo que hace se guarda en un sitio que se llama `CATALINA_HOME`  y `CATALINA_BASE`.

Cómo resumen,podríamos decir que sin Catalina, Tomcat sería como un coche sin motor: tendría ruedas y puertas, pero no se movería.

---
### Coyote

Coyote es el conector que recibe las peticiones de los usuarios (por ejemplo, cuando escribes una dirección en el navegador) y las entrega a Catalina para que las procese. Es como la “puerta de entrada” de Tomcat.

Actúa como la puerta de entrada para todas las peticiones que llegan desde los navegadores o clientes externos. 

Su función principal es escuchar esas solicitudes en un puerto específico, normalmente el 8080, y traducirlas a un lenguaje que Catalina pueda entender y procesar.

Se configura en el archivo `server.xml`, dentro de la carpeta `conf` de Tomcat, donde se definen los conectores y sus parámetros.

Como resumen podemos decir que es el componente que permite la interacción entre el servidor y los clientes.

---
### Jasper

Jasper es el componente de Tomcat que implementa la especificación JavaServer Pages (JSP). Su trabajo consiste en convertir las páginas JSP en código Java (servlets) y luego compilarlas para que Catalina pueda ejecutarlas.

Los servlets generados por Jasper se almacenan en el directorio `work` de Tomcat, mientras que su configuración se gestiona en los archivos de la carpeta `conf`, especialmente en `web.xml` y `server.xml`.

En resumen, Jasper es el motor que da vida a las páginas JSP dentro de Tomcat, transformándolas en servlets listos para ejecutarse.

---
### Manager y Host Manager

El Manager de Tomcat es una aplicación web que sirve para administrar las aplicaciones desplegadas en el servidor. Con él se pueden cargar nuevos archivos WAR, reiniciar aplicaciones, detenerlas o eliminarlas sin necesidad de reiniciar todo el servidor. 

También ofrece información sobre el estado de las aplicaciones, sesiones activas y recursos del sistema. Se accede normalmente a través de la URL `http://localhost:8080/manager/html` y su configuración de usuarios y roles se define en el archivo `conf/tomcat-users.xml`.

Por otro lado, el Host Manager es la aplicación que permite crear, eliminar y gestionar hosts virtuales dentro de Tomcat. Esto es útil cuando se quiere alojar varias aplicaciones o dominios en la misma instancia de servidor. 

Al Host Manager se accede mediante la URL `http://localhost:8080/host-manager/html` y, al igual que el Manager, requiere configurar roles y usuarios en `tomcat-users.xml`. Además, su configuración también se encuentra en los archivos XML dentro de la carpeta `conf/Catalina/localhost`.

---
### Estructura básica de directorios (bin, conf, webapps, lib, logs)

El directorio `bin` contiene los archivos ejecutables y scripts necesarios para iniciar y detener Tomcat, como **startup.sh** y **shutdown.sh**. 

El directorio `conf` guarda los archivos de configuración, siendo el más importante **server.xml**, donde se definen los conectores, hosts y demás parámetros del servidor. 

En `webapps` se ubican las aplicaciones web desplegadas, normalmente en forma de archivos **.war** o carpetas con la estructura de la aplicación. 

El directorio `lib` almacena las librerías Java (archivos .jar) que Tomcat necesita para funcionar y también las que pueden ser compartidas por todas las aplicaciones desplegadas. 

Finalmente, el directorio `logs` contiene los registros de actividad del servidor, incluyendo mensajes de inicio, errores y accesos, lo que resulta fundamental para la administración y el diagnóstico de problemas.

---
### Flujo interno de funcionamiento: recepción de peticiones, contenedores, despliegue de aplicaciones

El flujo interno de funcionamiento de Tomcat comienza cuando un usuario hace una petición desde su navegador. Esa solicitud llega primero al conector Coyote, que escucha en el puerto configurado y traduce la petición al lenguaje que entiende Tomcat. Luego, la petición se envía al contenedor principal Catalina.

Cuando la petición llega al contexto correcto, Catalina busca el servlet o la página JSP correspondiente. Si es una JSP, entra en acción Jasper, que la traduce a un servlet y la compila si es necesario. 

El servlet procesa la lógica de la aplicación y genera la respuesta. 

Finalmente, Catalina devuelve esa respuesta al conector Coyote, que la envía de vuelta al navegador del usuario.
