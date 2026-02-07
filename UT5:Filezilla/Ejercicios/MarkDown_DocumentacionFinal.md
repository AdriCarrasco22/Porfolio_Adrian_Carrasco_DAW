# 📝Filezilla: Documentación Final

## 1. Introducción
Este documento detalla el proceso para la implementación de un servicio de transferencia de archivos en nuestro entorno **Ubuntu** y su integración con **Apache**.

---

## 2. Instalación del Servidor
Para la gestión de archivos se hemos seleccionado **vsftpd** por su capacidad.

* **Comando de instalación:** `sudo apt update && sudo apt install vsftpd`
* **Gestión del servicio:** `sudo systemctl enable vsftpd` `sudo systemctl start vsftpd`

---

## 3. Configuración Básica
La configuración se ha realizado editando el archivo `/etc/vsftpd.conf`. Los parámetros más importantes establecidos son:

* `anonymous_enable=NO`: Bloqueo de acceso no autorizado.
* `local_enable=YES`: Permitir acceso a usuarios del sistema.
* `write_enable=YES`: Habilitar permisos de subida y modificación.
* `chroot_local_user=YES`: Implementación de "jaula" de seguridad para restringir al usuario a su directorio.

---

## 4. Usuarios y Permisos
Hemos configurado un entorno donde el usuario FTP coincide con el gestor de contenidos web.

* **Usuario:** `ftpuser`
* **DocumentRoot:** `/var/www/html`
* **Sincronización de permisos:**
    * Propietario: `ftpuser`
    * Grupo: `www-data`
    * Permisos: `755` para directorios y `644` para archivos, garantizando que el servidor web pueda servir el contenido.

---

## 5. Seguridad (FTPS)
Para evitar la interceptación de datos, se configuramos **FTP sobre TLS**:

1.  **Generación de certificado:** Uso de OpenSSL para crear una clave privada y un certificado autofirmado.
2.  **Configuración SSL:**
    * `ssl_enable=YES`
    * `force_local_data_ssl=YES` (Cifrado de archivos).
    * `force_local_logins_ssl=YES` (Cifrado de credenciales).

---

## 6. Modos de Conexión
### Modo Activo vs. Pasivo
Se ha priorizado el **Modo Pasivo** para evitar conflictos con Firewalls de cliente y NAT.

* **Configuración Pasiva:**
    * `pasv_min_port=50000`
    * `pasv_max_port=51000`
* **Justificación:** En el modo pasivo es el cliente quien inicia la conexión de datos, facilitando la comunicación a través de routers domésticos.

---

## 7. Clientes Utilizados
1.  **FileZilla:** Cliente principal para transferencias seguras mediante TLS.
2.  **Explorador de Archivos (Nautilus):** Test de compatibilidad básica y acceso rápido.
3.  **Navegador Web:** Validación de la publicación final mediante protocolo HTTP.

---

## 8. Integración Web
Se ha validado el flujo de despliegue mediante la subida de un archivo `practica10.html` por FTP y su posterior visualización en el navegador.

* **URL de acceso:** `http://10.0.2.15/practica10.html`


