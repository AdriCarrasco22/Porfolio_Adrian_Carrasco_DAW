# 📝Practica Tomcat: Identificación de archivos de configuración
 
Los archivos `conf/server.xml`, 
`conf/web.xml`, 
`conf/tomcat-users.xml`, 
`conf/context.xml` se encuentran en el directorio `$CATALINA_HOME/conf/`.  

A continuación vamos a explicar la función de cada archivo:

## Server.xml
Es el **archivo de configuración principal** de Tomcat. Define cómo se inicia el servidor, qué puertos usa, qué conectores están activos y cómo se estructuran los servicios internos.  

Entre los elementos que se pueden configurar encontramos:
-  Puertos, protocolos, número de hilos...
-  Nombre del motor de procesamiento de peticiones o autenticación
-  Virtual hosts o directorio de aplicaciones

## Web.xml
Es el **descriptor de despliegue global**. Define parámetros por defecto para todas las aplicaciones web desplegadas en Tomcat.  

Entre los elementos que se pueden configurar encontramos:
- Servlets y filtros por defecto
- Páginas de error globales
- Sesiones(tiempos de expiración)
- Seguridad

Cada aplicación también puede tener su propio `WEB-INF/web.xml`, pero este es el global.  

## Tomcat-users.xml
Define los **usuarios, roles y credenciales** que pueden acceder a las herramientas administrativas de Tomcat como `/manager` o `/host-manager`.  

Entre los elementos que se pueden configurar encontramos:
- Usuarios
- Roles
- Asignacion usuario-rol

## Context.xml
Define la **configuración** por defecto de los Contextos, es decir, **de cada aplicación web desplegada en Tomcat**.

Es una plantilla que se aplica a todas las apps, aunque cada aplicación puede tener su propio `META-INF/context.xml`.  

Entre los elementos que se pueden configurar encontramos:
- Recursos JNDI
- Parámetros de contexto
- Configuración de sesiones
- Rutas de logs
- Configuración de carga automática

## Mapa visual de dependencias de Tomcat
Para que todo lo investigado que hemos desarrollado en la practica quede de forma más clara, voy a explicarlo de una forma que considero sencilla:  

Tomcat es una **ciudad** y cada archivo es un **lugar importante** que hace que la ciudad funcione.

`TOMCAT(ciudad)` --- `server.xml(alcalde)` --- `context.xml(barrio)` --- `web.xml(normas)` --- `tomcat-users.xml(policia)` 

El `alcalde (server.xml)` decide como funciona la `ciudad (TOMCAT)`, abriendo los puertos para recibir solicitudes y organiza los `barrios (context.xml)`.  

Cada `barrio (context.xml)` es una aplicación web y se explica que necesita cada barrio (electricidad, agua, bases de datos...).  

Las `normas (web.xml)` son las reglas generales todos los barrios.  

Los `policias (tomcat-users.xml)` controlan quien puede entrar en las zonas importantes y se encargan de guardarf la identidad de cada habitante (usuario y contraseña).  

Como resumen general podemos decir que:
- `server.xml` manda sobre todo.
- `context.xml` depende de lo que diga server.xml.
- `web.xml` pone reglas que afectan a todos los contextos.
- `tomcat-users.xml` controla el acceso, pero no cambia cómo funciona la ciudad.
























