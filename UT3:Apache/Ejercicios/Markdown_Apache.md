# 📝Practica Apache: Introducción, Instalación y Configuración


## 1. Introducción

Esta práctica se va a desarrollar en un entorno de aprendizaje en el módulo de Despliegue de Aplicaciones Web impartido en 2°DAW.

Apache es un servidor web de código abierto, disponible para diversos sistemas operativos como Linux, Windows y macOS. Su función principal es atender las peticiones de los clientes mediante el protocolo HTTP y servir los contenidos solicitados, como páginas HTML.

El proyecto Apache nació en 1995 como una continuación del servidor NCSA HTTPd, que había sido uno de los primeros servidores web. Un grupo de desarrolladores decidió mejorar su funcionamiento y liberar la nueva versión bajo licencia libre. De ahí proviene su nombre, "a patchy server" (un servidor con parches).

Aunque Apache sigue siendo una opción muy extendida, existen otros servidores web que ofrecen distintas características:

- **Nginx**: conocido por su alto rendimiento y bajo consumo de recursos, muy usado en sitios de gran tráfico.

La elección entre uno u otro depende del tipo de proyecto y las necesidades de rendimiento o compatibilidad.

### 1.2 Motivación

El motivo principal de realizar este proyecto es aprender a instalar, configurar y comprender el funcionamiento del servidor Apache.

Trabajar con Apache es especialmente relevante porque continúa siendo la base de muchos servicios web actuales, tanto en entornos corporativos como en proyectos personales o educativos.

---

## 2. Relación de las actividades realizadas

### 2.1 Actualización del Sistema

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-1.png)  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-2.png)

### 2.2 Instalación de Apache

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-3.png)

### 2.3 Verificación de la instalación

Se comprobó la instalación mediante el comando `hostname -I`, mostrando las direcciones IP asignadas.

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-4.png)

### 2.4 Configurar el Usuario y grupo de Apache

Se editó el archivo `/etc/apache2/envvars` para asignar el usuario y grupo personalizados.  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-5.png)  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-6.png)

### 2.5 Configurar Directorio Raíz

Se configuró el archivo `/etc/apache2/apache2.conf` para definir el directorio raíz de documentos.  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-7.png)  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-8.png)


### 2.6 Habilitar módulos de Apache

Se habilitaron los módulos `headers` y `rewrite`, y se reinició el servicio.  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-9.png)  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-10.png)  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-11.png)  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-12.png)



### 2.7 Establecer Propiedades del Directorio de Documentos

Se asignaron permisos al directorio `/var/www/html`.  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-13.png)


### 2.8 Resultado Localhost navegador

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-14.png)


---

## 3. Configuración

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-15.png)


### 3.1 Crear nuestro sitio web

Se creó el directorio `/var/www/gci/` y un archivo `index.html` con contenido personalizado.

`sudo mkdir /var/www/gci/`
	
Ahora que tenemos un directorio creado para nuestro sitio, vamos a tener un archivo HTML en él. Vayamos a nuestro directorio recién creado y creemos uno escribiendo:

`cd /var/www/gci/`
`nano index.html`
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-16.png)  

Ahora vamos a crear un archivo VirtualHost para que aparezca cuando escribamos:

`gci.example.com`


---

## 4. Configuración del archivo de configuración de VirtualHost

Se copió y editó el archivo de configuración por defecto para crear `gci.conf`.

Entramos en el directorio de archivos de configuración:
`cd /etc/apache2/sites-available/`

`sudo cp 000-default.conf gci.conf`


Ahora vamos a editar el archivo de configuración:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-17.png) 


---

## 5. Activación del archivo VirtualHost
Después de configurar nuestro sitio web, necesitamos activar el archivo de configuración de hosts virtuales para habilitarlo.  

Se activó el sitio con `a2ensite gci.conf` y se recargó Apache.

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-18.png)   

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-19.png)   

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-20.png)   


---

## 6. Resultados

Con esta practica lo que se ha logrado es la obtención de conocimientos a la hora de instalar Apache.
Una vez instalado hemos creado una página por defecto a la que se accede cuando ejecutamos localhost y otra página la cual encontramos el mensaje de que esta funcionando correctamente.
Esta última página mencionada me ha dado algunos problemas ya que he tenido que añadir la dirección de la página al puerto de conexión correcto como podemos ver en esta captura:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes/img-21.png)   

En cuanto a otros problemas/inconvenientes, he de decir que no me he encontrado con ninguno más y la practica me ha salido de forma fluida y rápida.

En cuanto a la valoración personal, creo que esta práctica ha significado mucho para mi en cuanto al uso y manejo de la terminal de Ubuntu ya que mis conocimientos hasta ahora eran muy escasos.


---

## 7. Bibliografía

https://foro.puntocomunica.com/viewtopic.php?t=312

https://www.reddit.com/r/apache/comments/nrsfbg/cant_open_sample_gciexamplecom/

https://discourse.ubuntu.com/t/install-and-configure-apache/13955/2

