# 📝Practica Apache HTTPS
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/imgPortada.png)  

## 1. Funcionamiento de HTTPS y su importancia

Cuando usamos Internet, normalmente escribimos direcciones como www.algo.com y enviamos información.  
Si la página no es segura, cualquiera podrá ver lo que escribimos o mandamos.

Para evitar eso, se inventó HTTPS, que significa **HyperText Transfer Protocol Secure** (la información viaja cifrada).

### 1.1 ¿Por qué HTTPS?

- Protege tu privacidad.  
- Demuestra que la web es auténtica.  
- Es obligatorio en páginas que usan contraseñas, pagos o información personal.

---

## 2. Certificados SSL y TLS

### 2.1 Certificados Autofirmados

Los certificados autofirmados son los generados y firmados por la misma persona u organización que los usa.

**Ventajas:**
- Gratuitos y fáciles de crear.  
- Útiles para entornos internos o pruebas.  

**Desventajas:**
- No están validados por una CA reconocida.  
- Son vulnerables a ataques de suplantación.  
- Pueden generar desconfianza en usuarios finales.  

### 2.2 Certificados emitidos por una CA confiable

Como su propio nombre indica, son los firmados por una Autoridad de Certificación 	reconocida.

**Ventajas:**
- Reconocidos automáticamente por navegadores y sistemas operativos.
- Garantizan autenticidad y confianza en la identidad del sitio web.
- Reducen riesgos de phishing (ciberataques de ingeniería social en el que los delincuentes se hacen pasar por entidades legítimas) y ataques de intermediarios (MITM).

**Desventajas:**
- Pueden tener coste económico (aunque existen opciones gratuitas).  
- Requieren un proceso de validación que puede ser complejo. 

---

## 3. Módulos de Apache necesarios para habilitar SSL/TLS en Ubuntu

En Ubuntu, para habilitar SSL/TLS en Apache2 necesitas principalmente el módulo `mod_ssl`.  
También se suele habilitar `mod_headers` y `mod_socache_shmcb`.

---

## 4. Ejecución práctica de la actividad

### ACTUALIZACIÓN DE LOS REPOSITORIOS DEL SISTEMA

```bash
sudo apt update
```
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img1.png)

---

### INSTALACIÓN DE APACHE2

```bash
sudo apt install apache2 -y
```
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img2.png)

Como ya lo habíamos instalado en practicas anteriores, vemos que no se instalará nada.

---

### VERIFICACIÓN DE QUE EL SERVICIO SE HA INSTALADO CORRECTAMENTE

```bash
apache2 -v
```
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img3.png)

---

### COMPROBACIÓN SI EL SERVICIO APACHE2 ESTÁ ACTIVO

```bash
systemctl status apache2
```

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img4.png)

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img5.png)
Como vemos, Apache2 se encuentra activo en nuestra Máquina Vitual.

---

### HABILITACIÓN DE MÓDULOS NECESARIOS

```bash
sudo a2enmod ssl
sudo a2enmod headers
sudo a2enmod socache_shmcb
systemctl restart apache2
```
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img6.png)

---

### 4.1 Generar un certificado SSL/TLS (Autofirmado)

#### OPCIÓN A: CERTIFICADO AUTOFIRMADO

Emplearemos los siguientes comandos:

```bash
sudo mkdir /etc/apache2/ssl
cd /etc/apache2/ssl
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout apache.key -out apache.crt
```

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img7.png)

---

### 4.2 Configuración de VirtualHost HTTPS en el puerto 443

Para la creación del archivo de sitio HTTPS hemos utilizado el siguiente comando:
`sudo nano/etc/apache2/sites-available/miweb-ssl.conf`

Posteriormente, en el archivo que hemos creado, hemos insertado este texto: 

```apache
<VirtualHost *:443>
    ServerName miweb.local
    DocumentRoot /var/www/html

    SSLEngine on
    SSLCertificateFile /etc/apache2/ssl/apache.crt
    SSLCertificateKeyFile /etc/apache2/ssl/apache.key

    # Cabeceras de seguridad básicas
    Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
    Header always set X-Content-Type-Options "nosniff"
    Header always set X-Frame-Options "DENY"

    <Directory /var/www/html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/ssl_error.log
    CustomLog ${APACHE_LOG_DIR}/ssl_access.log combined
</VirtualHost>
```
Después hemos habilitado el sitio en Apache con este comando:

```bash
sudo a2ensite miweb-ssl.conf
```
Finalmente hemos comprobado la configuración y este ha sido el resultado:
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img8.png)

---

## REDIRECCIÓN DE HTTP A HTTPS
Primero he editado el VirtualHost de puerto 80:
`/etc/apache2/sites-available/000-default.conf`

Posteriormente, dentro de este archivo hemos tenido que modificar ciertas líneas 	quedando 	como resultado:

```apache
<VirtualHost *:80>
    ServerName miweb.local
    Redirect "/" "https://miweb.local/"
</VirtualHost>
```
Finalmente probamos la configuración y vemos que todo ha salido bien:
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img9.png)

---

## REINICIO O RECARGA DE APACHE
Una vez hemos realizado los anteriores paso, vamos a proceder al reinicio de Apache para comprobar la funcionalidad de los cambios realizados anteriormente.
### Recarga
```bash
sudo systemctl reload apache2
```

### VER EL ESTADO DEL SERVICIO

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img11.png)

---
## VER LOGS SI ALGO FALLA

```bash
sudo journalctl -u apache2 --since "10 minutes ago"
sudo tail -n 100 /var/log/apache2/error.log
```


![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img12.png)

---

## VALIDACIÓN DE LA IMPLEMENTACIÓN

### Con el navegador

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img13.png)
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img14.png)
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img15.png)

### Con CURL

```bash
curl -I -k https://miweb.local
```

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img16.png)
![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img17.png)

### Con OPENSSL

```bash
openssl s_client -connect miweb.local:443 -servername miweb.local -showcerts </dev/null
```

![img](https://github.com/AdriCarrasco22/Porfolio_Adrian_Carrasco_DAW/blob/main/UT3%3AApache/Ejercicios/Imagenes_HTTPS/img18.png)


