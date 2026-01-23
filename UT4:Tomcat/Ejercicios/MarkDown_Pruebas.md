# 📝Pruebas de Funcionamiento y Rendimiento

## 1. Utilización de Herramientas

### ApacheBench
Este herramienta esta includia en el paquete `apache2-utils` y la instalaremos con el siguiente comando:    
`sudo apt install apache2-utils`  

Para realizar la prueba con esta herremienta ya instalada ejecutaremos el siguiente comando:  
`ab -n 1000 -c 50 http://localhost:8080/manager/html`  

Como resultado obtendremos:  
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img1_actividadPruebas.png)

### Curl
En segundo lugar vamos a realizar las pruebas con esta herramienta y no tendremos que ejecutar ningún comando ya que la encontramos disponible por defento en Ubuntu:  

Para realizar la prueba con esta herramienta vamos a ejecutar el siguiente comando:  
`seq 1 100 | xargs -n1 -P20 curl http://www.google.com/`  

Como resultado veremos que se nos va a mostrar JSON, HTML y texto de la respuesta (todo mezclado) ya que es paralelo.  
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img2_actividadPruebas.png) 

### JMeter
Por último, vamos a realizar las pruebas con esta herramienta gráfica la cual instalararemos mediante:  
`sudo apt install jmeter`  
Para comprobar el resultado de esta prueba me he creado un **Plan de Pruebas** en el que vamos a obtener:  
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img3_actividadPruebas.png)  

## 2. Ajustes realizados en el fichero `server.xml`  
Vamos a modificar este archivo añadiendo este contenido:  
`<Connector
    port="8080"
    protocol="org.apache.coyote.http11.Http11NioProtocol"
    maxThreads="300"
    minSpareThreads="50"
    acceptCount="100"
    connectionTimeout="10000"
    enableLookups="false"
    redirectPort="8443" />
`  
## 3. Pruebas después de los ajustes

### ApacheBench
Una vez hemos efectuado todos los ajustes que hemos considerados necesarios vamos a ver los resultados que se nos muestran al ejecutar las pruebas:  
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img4_actividadPruebas.png)  

### Curl
Con esta herramienta una vez que ejecutamos el comando de nuevo vamos a encontrar como respuesta:  
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img5_actividadPruebas.png)  
Como vemos, de nuevo será un fichero que incluye JSON, HTML y el texto de respuesta.

### JMeter
Con esta herramienta una vez que ejecutamos el comando de nuevo vamos a encontrar como respuesta:  
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img6_actividadPruebas.png)

## 4. Conclusión
Como conclusión puedo decir que:  

-  Tomcat responde correctamente a pruebas de carga en Ubuntu.
-  La configuración por defecto no está optimizada para alta concurrencia.
-  Ajustar hilos, tiempos de espera y cola de conexiones mejora significativamente el rendimiento.
-  ApacheBench y JMeter son herramientas eficaces para detectar cuellos de botella.
-  Tras los ajustes, el servidor soporta mayor carga con menor latencia.












