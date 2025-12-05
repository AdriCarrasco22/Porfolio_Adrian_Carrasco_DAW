

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

Firmados por una Autoridad de Certificación reconocida.

**Ventajas:**
- Reconocidos automáticamente por navegadores y sistemas operativos.  
- Garantizan autenticidad y confianza.  
- Reducen riesgos de phishing y ataques MITM.  

**Desventajas:**
- Pueden tener coste económico (aunque existen opciones gratuitas).  
- Requieren un proceso de validación más complejo.  

---

## 3. Módulos de Apache necesarios para habilitar SSL/TLS en Ubuntu

En Ubuntu, para habilitar SSL/TLS en Apache2 necesitas principalmente el módulo **mod_ssl**.  
También se suele habilitar **mod_headers** y **mod_socache_shmcb**.

---

## 4. Ejecución práctica de la actividad

### ACTUALIZACIÓN DE LOS REPOSITORIOS DEL SISTEMA

[Imagen3]

---

### INSTALACIÓN DE APACHE2

```bash
sudo apt install apache2 -y
```

---

### VERIFICACIÓN DE QUE EL SERVICIO SE HA INSTALADO CORRECTAMENTE

| Comando | Resultado |
|---------|-----------|
| `apache2 -v` | Server version: Apache/2.4.58 (Ubuntu) |

---

### COMPROBACIÓN SI EL SERVICIO APACHE2 ESTÁ ACTIVO

```bash
systemctl status apache2
```

[Imagen4]

---

### HABILITACIÓN DE MÓDULOS NECESARIOS

```bash
sudo a2enmod ssl
sudo a2enmod headers
sudo a2enmod socache_shmcb
systemctl restart apache2
```

---

### 4.1 Generar un certificado SSL/TLS (Autofirmado)

```bash
sudo mkdir /etc/apache2/ssl
cd /etc/apache2/ssl
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout apache.key -out apache.crt
```

[Imagen5]

---

### 4.2 Configuración de VirtualHost HTTPS en el puerto 443

Archivo: `/etc/apache2/sites-available/miweb-ssl.conf`

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

---

## REDIRECCIÓN DE HTTP A HTTPS

Archivo: `/etc/apache2/sites-available/000-default.conf`

```apache
<VirtualHost *:80>
    ServerName miweb.local
    Redirect "/" "https://miweb.local/"
</VirtualHost>
```

---

## REINICIO O RECARGA DE APACHE

```bash
sudo systemctl reload apache2
```

---

## VER EL ESTADO DEL SERVICIO

[Imagen6]

---

## VER LOGS SI ALGO FALLA

```bash
sudo journalctl -u apache2 --since "10 minutes ago"
sudo tail -n 100 /var/log/apache2/error.log
```

[Imagen7]

---

## VALIDACIÓN DE LA IMPLEMENTACIÓN

### Con el navegador

[Imagen8]

### Con CURL

```bash
curl -I -k https://miweb.local
```

[Imagen9]

### Con OPENSSL

```bash
openssl s_client -connect miweb.local:443 -servername miweb.local -showcerts </dev/null
```

[Imagen10]

---

Realizado por Adrián Carrasco Fernández  
2ºDAW  
Desarrollo de Aplicaciones Web
```
