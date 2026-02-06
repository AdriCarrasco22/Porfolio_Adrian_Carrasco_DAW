# 📝Filezilla: Uso del navegador como Cliente FTP

## 1. Acceso desde el navegador

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img1_actividadNavegador.png)  

He intentado acceder mediante el protocolo FTP nativo, pero debido a que los navegadores modernos 
han eliminado el soporte de FTP por seguridad, el navegador no puede renderizar 
el contenido directamente. Esto demuestra que para el despliegue de aplicaciones es obligatorio el uso 
de clientes dedicados como FileZilla.


## 2. Solución ante el problema anterior

Para poder realizar esta actividad, vamos a abrir en primer lugar el gestor de archivos.  

Una vez lo hayamos abierto, en la columna de la izquierda, al final de la lista, haremos click en **+ Otras ubicaciones**.  

En la parte inferior aparece un cuadro de texto que dice **"Conectar al servidor"**. Ahí vamos a escribir nuestra dirección ftp
con la que accederemos: `ftp://10.0.2.15` y pulsaremos el boton de conectar.  

Se nos abrirá esta ventana emergente donde tendremos que hacer la autenticación de nuestro usuario y contraseña:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img2_actividadNavegador.png) 

Ahora vemos el contenido de nuestro servidor FTP como si fuera una carpeta local de nuestro ordenador.  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img3_actividadNavegador.png)  


## 3. Ventajas y Desventajas

  * **Ventajas de usar el explorador de archivos frente a un navegador:**
      * **Integración:** Permite copiar, pegar, arrastrar y soltar archivos como si estuvieras en tu propio disco duro.
      * **Edición directa:** En algunos casos, puedes abrir un archivo de texto directamente con gedit, editarlo y, al guardar, se sube automáticamente al servidor.
      * **Comodidad:** No necesitas aprender a usar una interfaz compleja como la de FileZilla para operaciones rápidas.

  * **Desventajas frente a un cliente dedicado (FileZilla):**
      * **Falta de información técnica:** No puedes ver los códigos de respuesta del servidor ni depurar errores de conexión.
      * **Gestión de certificados:** Los exploradores de archivos suelen dar problemas con el FTPS (FTP seguro) que configuramos antes, prefiriendo conexiones no cifradas o fallando si el certificado es autofirmado.
      * **Rendimiento:** Para transferir cientos de archivos pequeños (como un proyecto web de Node o PHP), es mucho más lento e inestable que FileZilla.

## 4. Conclusión
El uso del navegador o del explorador de archivos como cliente FTP es una solución rápida pero limitada para el despliegue de aplicaciones.

A diferencia de los clientes dedicados como FileZilla, estas herramientas tienen tres debilidades/carencias:

  * **Incompatibilidad de Seguridad:** Los navegadores modernos han eliminado el soporte FTP nativo, y los exploradores de archivos fallan ante configuraciones de FTPS (TLS/SSL), obligando a reducir la seguridad del servidor para permitir el acceso.
  * **Funcionalidad Unidireccional:** Están orientados principalmente a la descarga y visualización, careciendo de herramientas de gestión avanzada como edición de permisos (chmod), gestión de colas de subida o monitorización de logs en tiempo real.
  * **Inestabilidad:** Son propensos a errores de conexión (como el "final de flujo inesperado") al no gestionar correctamente los certificados autofirmados o los puertos pasivos.
