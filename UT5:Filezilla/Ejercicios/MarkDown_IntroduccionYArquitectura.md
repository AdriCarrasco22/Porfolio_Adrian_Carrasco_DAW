# 📝Filezilla: Introducción y arquitectura de Filezilla Server
## 1. Introducción al servidor FTP / FTPS

Un servidor `FTP (File Transfer Protocol)` es un servicio que permite la transferencia de archivos entre un cliente y un servidor a través de una red TCP/IP. Este protocolo sigue un modelo cliente–servidor, en el cual el cliente inicia la conexión y solicita operaciones como listar directorios, subir o descargar archivos.

FTP, en su forma original, no cifra la información, por lo que tanto las credenciales como los datos viajan en texto plano. Para solucionar este problema surge `FTPS`, que es FTP con cifrado SSL/TLS. Por otro lado, `SFTP` es un protocolo distinto que funciona sobre SSH y no forma parte de la familia FTP.


## 2. Diferencias conceptuales entre FTP, FTPS y SFTP

`FTP utiliza conexiones TCP sin cifrado`, generalmente sobre el puerto 21, lo que lo hace inseguro en redes no confiables. `FTPS añade una capa de seguridad mediante SSL/TLS`, manteniendo la misma estructura de funcionamiento de FTP, pero protegiendo las comunicaciones. `SFTP se basa en SSH y utiliza un único canal cifrado`, normalmente sobre el puerto 22, por lo que no comparte arquitectura ni funcionamiento con FTP/FTPS.  


## 3. Arquitectura cliente–servidor en FTP

La arquitectura de FTP se basa en dos entidades principales: **el cliente FTP**, que inicia la comunicación, y **el servidor FTP**, que atiende las solicitudes. A diferencia de otros protocolos, FTP utiliza dos canales de comunicación independientes:

  * Un canal de control, que permanece abierto durante toda la sesión.

  * Un canal de datos, que se abre y se cierra cada vez que se transfieren archivos o se listan directorios.

Esta separación permite gestionar comandos y transferencias de forma independiente.  


## 4. Canal de control

El canal de control es el encargado de `la autenticación del usuario y del envío de comandos FTP`. Este canal se establece al inicio de la sesión y se mantiene activo hasta que el cliente se desconecta. Por defecto, el servidor escucha en el `puerto TCP 21`.

A través de este canal se envían instrucciones como el inicio de sesión, solicitudes de listado de directorios y órdenes de transferencia. No se utiliza para transportar datos de archivos, sino únicamente para control de la sesión.  


## 5. Canal de datos

El canal de datos se utiliza exclusivamente para `la transferencia de información, como archivos o listados de directorios`. A diferencia del canal de control, este canal no es permanente, sino que se abre y se cierra cada vez que se realiza una operación de transferencia.

El comportamiento del canal de datos depende del modo de funcionamiento del protocolo FTP: modo activo o modo pasivo.  


## 6. Funcionamiento del modo activo

En el modo activo, `el cliente establece primero la conexión de control con el servidor a través del puerto 21`. Posteriormente, el cliente indica al servidor en qué puerto local está preparado para recibir datos. Cuando se inicia una transferencia, el servidor abre una conexión de datos desde su puerto TCP 20 hacia el puerto indicado por el cliente.

Este modo presenta **problemas en entornos con firewalls o NAT**, ya que el cliente debe aceptar conexiones entrantes desde el servidor, lo cual suele estar bloqueado por razones de seguridad.  


## 7. Funcionamiento del modo pasivo

En el modo pasivo, el cliente establece la conexión de control con el servidor de la misma forma que en el modo activo. Sin embargo, `cuando se requiere una transferencia de datos, el servidor informa al cliente de un puerto disponible dentro de un rango previamente configurado`. El cliente es quien inicia la conexión hacia ese puerto del servidor.

`Este modo es el más utilizado actualmente`, ya que evita problemas con firewalls y permite que todas las conexiones sean iniciadas por el cliente, lo que resulta más compatible con redes modernas.  


## 8. Puertos implicados en FTP

`FTP utiliza el puerto 21` para el canal de control de manera estándar. En el modo activo, el canal de datos se origina desde el puerto 20 del servidor. En el modo pasivo, el canal de datos utiliza un rango de puertos configurables en el servidor, que deben estar abiertos para permitir las transferencias.

La correcta configuración de estos puertos es fundamental para garantizar el funcionamiento del servicio FTP, especialmente en entornos con medidas de seguridad estrictas.  


## 9. Conclusión

Como conclusión, podemos decir que el protocolo FTP se caracteriza por su `arquitectura cliente–servidor` y por el `uso de dos canales de comunicación independientes`. La distinción entre canal de control y canal de datos, así como entre modo activo y modo pasivo, es clave para comprender su funcionamiento.
