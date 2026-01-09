# 📝Despliegue de una simple Aplicación Web

## 1. Descarga del archivo de aplicación (WAR)

He optado por utilizar un archivo oficial de Apache Tomcat. Para descargarlo he utilizado el siguiente comando:  

`wget https://tomcat.apache.org/tomcat-9.0-doc/appdev/sample/sample.war`.  

## 2. Despliegue en la carpeta "webapps"
El despliegue se realiza aprovechando la característica de `Auto-Deploy` de Tomcat, la cual permite que el servidor identifique y despliegue aplicaciones web sin necesidad de reiniciarlo. Posteriormente, se mueve el archivo descargado al directorio donde el servidor busca aplicaciones para publicar.

**Comando de despliegue**
`sudo cp sample.war /var/lib/tomcat10/webapps/`  

**Verificación del contenido en el directorio**
`ls -l /var/lib/tomcat10/webapps/`  

## 3. Análisis del proceso interno de Tomcat
Al controlar los logs del sistema mediante `sudo tail -f /var/log/tomcat10/catalina.out`, se han identificado los siguientes pasos internos realizados por el servidor:

- **Detección (Scanner)**: El hilo de ejecución de fondo de Tomcat (background processor) detecta la presencia de un nuevo archivo en el directorio `webapps`.

- **Validación y Expansión**: Tomcat verifica la integridad del archivo `.war` y lo descomprime en una carpeta con el mismo nombre.
- **Carga de Contexto**: Se lee el archivo de configuración interna `WEB-INF/web.xml` para establecer los parámetros de la aplicación.
- **Escaneo de Clases y TLDs**: El cargador de clases (ClassLoader) registra los Servlets y escanea las librerías de etiquetas JSP (TLDs).
- **Registro de URL**: La aplicación se vincula a una ruta de contexto, en este caso `/sample`, y queda lista para recibir peticiones HTTP.

## 4. Evidencia de acceso a la aplicación
Para verificar el despliegue, se accede a la aplicación a través del navegador utilizando la dirección IP del servidor o localhost:  
`http://localhost:8080/sample/`.  

Como resultado final encontramos:
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img1_actividad3.png)
