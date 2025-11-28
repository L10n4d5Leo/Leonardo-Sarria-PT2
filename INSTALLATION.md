# Primero abrimos la terminal y hacemos esto dentro...
- Actualitza el sistema con "sudo apt update && sudo apt upgrade -y"
- Despues Instala Apache con "sudo apt install apache2 -y"
- Ahora activamos e iniciamos el servicio 
- Ahora activamos e iniciamos el servicio con "sudo systemctl enable apache2" y "sudo systemctl start apache2"
- Y lo verificas con "sudo systemctl status apache2"
  # Procedemos a instalar MySQL
- primero esto "sudo apt install mysql-server mysql-client -y"
- desapues iniciamos y habilitamos el sistema "sudo systemctl enable mysql" "sudo systemctl start mysql"
- accedemos a la consola de MySQL "sudo mysql"
- creamos la base de dades "CREATE DATABASE bbdd;"
- ahora creamos el usuario local "CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'; GRANT ALL PRIVILEGES ON bbdd.* TO 'usuario'@'localhost'; FLUSH PRIVILEGES; EXIT;"
  # Ahora instalamos la PHP  y otras extensiones comunes
- "sudo apt install php libapache2-mod-php php-mysql php-curl php-gd php-mbstring php-xml php-zip php-json php-cli -y"
- reiniciamos APACHE para cargar PHP "sudo systemctl restart apache2"
- verificamos la version de PHP "php -v"
- creamos un fitxer de prueba "echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php"
- visitamos "http://localhost/info.php" para ver la informacion PHP
# verificaion final 
- La pila LAMP ahora debería estar operativa con
- Apache sirviendo páginas web.
- MySQL preparado para almacenar datos.
- PHP procesando scripts.
# Configuración de VirtualHost con apache2
# Aqui debeis cambiar todo lo que veas que diga "domini" por un nombre que tu elijas
# Creacion de la estructura de directorios 
- Crearemos un directorio ejemplo "domini.local"  en vuestro caso cambiaias el domini por lo que querais. aqui esta "sudo mkdir -p /var/www/domini.local"
# Definicion del VirtualHost
- creais un fitxer para vuestro virtualhost "sudo nano /etc/apache2/sites-available/domini.local.conf"
- aqui cambiais todo lo que diga domini
- "<VirtualHost *:80>
    ServerAdmin admin@domini.local
    ServerName www.domini.local
    ServerAlias domini.local
    DocumentRoot /var/www/domini.local
    ErrorLog ${APACHE_LOG_DIR}/domini.local_error.log
    CustomLog ${APACHE_LOG_DIR}/domini.local_access.log combined
</VirtualHost>"
- habilitamos el virtualhost "sudo a2ensite domini.local.conf"
- reiniciamos apache "sudo systemctl restart apache2"
- modificamos etc/hosts para resolver el dominio localmente "sudo nano /etc/hosts"
- y esto "127.0.0.1   www.domini.local domini.local"
- comprobamos si funciona "http://www.domini.local" con el nombre que elegiste
- Si el directorio /var/www/domini.local está vacío, Apache puede mostrar un error 403 o una lista de directorios (según la configuración). Para probar que funciona, cree un archivo de prueba con esto "echo "<h1>Hola, benvingut domini.local</h1>" | sudo tee /var/www/domini.local/index.html"
# Asignacion de permisos 
- canviar el propietario "sudo chown -R $USER:www-data /var/www/domini.local"
- establecer los permisos "sudo chmod -R 775 /var/www/domini.local"
  # Pasos clave
- Crear directorio     "sudo mkdir -p /var/www/domini.local"
- Configurar VirtualHost   "Editar  "/etc/apache2/sites-available/domini.local.conf"
- Habilitar sitio          "sudo a2ensite domini.local.conf"
- Reiniciar Apache         "sudo systemctl restart apache2"
- Añadir dominio a hosts   "127.0.0.1 www.domini.local en /etc/hosts"
- Verificar permisos       "chown y chmod como se indica"
- Depurar errores          "Consultar error.log y access.log"
# Guía de instalación y configuración de plataformas cloud (Nextcloud / ownCloud)
- descargar e instala la plataforma cloud
- Nextcloud: https://download.nextcloud.com/server/releases/latest.zip
- ownCloud: https://download.owncloud.com/server/stable/owncloud-complete-20240724.zip
- Muévete al directorio del virtual host "cd /var/www/domini.local"
- limpieza del contenido actual "sudo rm -rf *"
- descarga el fitxer de la plataforma que elegiste "wget https://download.nextcloud.com/server/releases/latest.zip"
- descomprime el archivo directamente en el directorio "sudo unzip /ruta/al/arxiu.zip" "sudo mv nextcloud/* . && sudo rmdir nextcloud" "sudo mv owncloud/* . && sudo rmdir owncloud"
- haceis esto si lo teneis descomprimido en descargas "cp -R ~/Descargas/nextcloud/. /var/www/domini.local/."
- eliminais la carpeta "sudo rm -rf ~/Descargas/nextcloud && sudo rm -rf ~/Descargas/latest.zip"
- haceis esto si lo teneis descomprimido en "cp -R /var/www/domini.local/nextcloud/. /var/www/domini.local/."
- eliminais "sudo rm -rf /var/www/domini.local/nextcloud && sudo rm -rf /var/www/domini.local/latest.zip"
- aseguramos los permisos correctos "sudo chown -R www-data:www-data /var/www/domini.local"  "sudo chmod -R 755 /var/www/domini.local"
- accedes a la interfaz web "http://domini.local"
- Recomendaciones adicionales
-  Directorio de datos: Durante la instalación, se recomienda no almacenar los datos dentro del directorio web (ej: /var/www/domini.local/data). Mejor utiliza una ruta externa como /var/ncdata o /opt/owncloud-data
- Copias de seguridad: Realiza backups regulares del directorio de datos y de la base de datos.
- seguridad: Desactiva el acceso a archivos sensibles (.htaccess, config.php) y considera añadir reglas de seguridad adicionales a Apache o Nginx.
# Apéndice: Instalación de PHP 7.4 en Ubuntu 24.04 (sólo para ownCloud)
- actualiza el sistema "sudo apt update && sudo apt upgrade -y"
- instala las dependencias para elegir repositorios PPA "sudo apt install software-properties-common -y"
- Añade el repositorio de PHP de Ondřej Surý "LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php -y"
- Actualiza los repositorios "sudo apt update"
- Instala PHP 7.4 y las extensiones requeridas
- "sudo apt install -y php7.4 \
    libapache2-mod-php7.4 \
    php7.4-fpm \
    php7.4-common \
    php7.4-mbstring \
    php7.4-xmlrpc \
    php7.4-soap \
    php7.4-gd \
    php7.4-xml \
    php7.4-intl \
    php7.4-mysql \
    php7.4-cli \
    php7.4-ldap \
    php7.4-zip \
    php7.4-curl"
  - (Opcional) Selecciona PHP 7.4 como versión predeterminada "sudo update-alternatives --config php"
  - Activa los módulos de Apache necesarios "sudo a2enmod proxy_fcgi setenvif "sudo a2enconf php7.4-fpm"
  - reinicia APACHE "sudo systemctl restart apache2"
  - Verificació: Pots comprovar la versió activa de PHP amb "php -v"

