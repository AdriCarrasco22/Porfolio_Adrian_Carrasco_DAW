# 📝Filezilla: Pruebas con clientes gráficos

## 1. Instalación de FileZilla Client
En primer lugar vamos a instalar filexilla en nuestra Máquina de Ubuntu si no lo tuvieramos ya instalado:  

`sudo apt update `  

`sudo apt install filezilla`  

Una vez hayamos instalado filezilla, lo abriremos mediante el siguiente comando : `filezilla`.  

Nos aparecerá esto por pantalla:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img1_actividadClienteGrafico.png)


## 2. Configurar una conexión guardada
Abriremos el Administrador de sitios: **Archivo → Gestor de sitios → Nuevo sitio** .

A continuación configuraremos los datos:  

`Protocolo	FTP – Protocolo de Transferencia de Archivos`

`Servidor	10.0.2.15 (la IP de tu VM Ubuntu donde corre vsftpd)`

`Puerto	21 (puerto FTP por defecto)`

`Cifrado	Usar FTP explícito sobre TLS si está disponible para pruebas con seguridad`

`Modo de acceso	Normal`

`Usuario	usuario1 `

`Contraseña	La contraseña que configuré para usuario1` 

Una vez hayamos configurado los datos le daremos a **Conectar** y si todo ha ido bien nos deberá aparecer lo siguiente:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img2_actividadClienteGrafico.png)  


## 3. Realizar transferencia bidireccional

  * **Subir un archivo**
    Arrastramos un archivo al directorio remoto (/srv/ftp/limitado).  
    FileZilla mostrará en la ventana de estado:

    `Comenzando transferencia...
    Transferencia completa`

  * **Descargar archivo**
    Arrastramos un archivo desde el servidor al PC
    Observaremos los mismos mensajes en la ventana de estado.

    
## 4. Observar mensajes de estado
En la ventana de estado en FileZilla se muestra cada comando FTP enviado y la respuesta del servidor:  

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT5%3AFilezilla/Ejercicios/Imagenes/img3_actividadClienteGrafico.png)  


## 5. Conclusión

He  realizado pruebas con FileZilla Client conectándome al servidor FTP. 
Configuré una conexión guardada con la IP 10.0.2.15, usuario y contraseña. 
Reralicé transferencias bidireccionales de archivos, subiendo y descargando ficheros 
entre la máquina local y el servidor. La ventana de estado de FileZilla ha muestrado la secuencia de comandos 
y respuestas del servidor, confirmando que las transferencias se completaron correctamente y que 
el servidor responde a las operaciones gráficas.

