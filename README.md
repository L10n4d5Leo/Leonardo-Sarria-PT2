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
