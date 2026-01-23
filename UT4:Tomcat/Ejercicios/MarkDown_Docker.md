# 📝Tomcat en contenedores (Docker)

## 0. ¿Qué es Docker?
**Docker** permite ejecutar aplicaciones dentro de contenedores, que incluyen:

- La aplicación
- Sus dependencias
- El entorno necesario

Con Tomcat, Docker permite desplegar rápidamente el servidor sin instalarlo directamente en el sistema.  

## 1. Instalación de Docker
En primer lugar vamos a comprobar si ya tenemos instalado Docker mediante `docker --version`. De no estar instalado ejecutaremos:
- `sudo apt install docker.io`
- `sudo systemctl start docker`
- `sudo systemctl enable docker`

## 2. Descarga de la imágen oficial de Tomcat
Descargaremos la imagen ficial de TOmcat tal y como se nos muestra en la actividad:  
`docker pull tomcat:latest`  
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT4%3ATomcat/Ejercicios/Imagenes/img1_actividadDocker.png)

## 3. Ejecución de Tomcat en un contenedor
En este apartado vamos a probar a lanzar Tomcat desde un contenedor montando un volumen lo cual nos permite modificar la app sin recrear el contenedor:  
`docker run -d \
-p 8080:8080 \
-v $(pwd)/webapps:/usr/local/tomcat/webapps \
--name tomcat-volumen \
tomcat:latest
`  

Durante el despliegue de Tomcat en Docker se produjo un conflicto de puertos, ya que el puerto 8080 se encontraba en uso por una instancia de Tomcat instalada de forma nativa en el sistema. Para solucionarlo, se asignó un puerto alternativo en el host.  

## 4. Diferencias entre Tomcat nativo y Tomcar en contenedor

- **Tomcat nativo**
  
  - Se instala directamente en el sistema
  - Usa librerías del sistema operativo
  - Requiere configuración manual (Java, variables, rutas)
  - Es más difícil de replicar en otros equipos
  - Puede dejar residuos en el sistema
 
- **Tomcat en contenedor (Docker)**
- 
  - No requiere instalación directa de Tomcat ni Java
  - Entorno aislado y reproducible
  - Despliegue rápido y portátil
  - Fácil eliminación y recreación
  - Ideal para pruebas, CI/CD y cloud
  - Ligera sobrecarga por Docker
  - Persistencia de datos requiere volúmenes

## 5. Conclusión
El uso de Tomcat en contenedores Docker simplifica notablemente el despliegue y mantenimiento del servidor de aplicaciones, ofreciendo un entorno aislado, reproducible y fácilmente escalable frente a la instalación tradicional de Tomcat en el sistema operativo.
