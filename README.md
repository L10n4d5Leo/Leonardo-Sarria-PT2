 Primero abrimos la terminal y hacemos esto dentro...
- Actualitza el sistema con "sudo apt update && sudo apt upgrade -y"
- Despues Instala Apache con "sudo apt install apache2 -y"
- Ahora activamos e iniciamos el servicio 
- Ahora activamos e iniciamos el servicio con "sudo systemctl enable apache2" y "sudo systemctl start apache2"
- Y lo verificas con "sudo systemctl status apache2"
  # Procedemos a instalar MySQL
- primero esto "sudo apt install mysql-server mysql-client -y"
