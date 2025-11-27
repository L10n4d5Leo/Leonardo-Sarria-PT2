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



v 
