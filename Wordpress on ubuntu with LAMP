Bash script that automates the installation of WordPress with LAMP on Ubuntu Server:

#!/bin/bash

# Update package lists
sudo apt update

# Install Apache
sudo apt install -y apache2

# Install MySQL
sudo apt install -y mysql-server

# Secure MySQL installation
sudo mysql_secure_installation <<EOF

y
password
password
y
y
y
y
EOF

# Install PHP
sudo apt install -y php libapache2-mod-php php-mysql

# Restart Apache
sudo systemctl restart apache2

# Download and extract WordPress
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -zxvf latest.tar.gz

# Move WordPress files to Apache root directory
sudo mv wordpress/* /var/www/html/

# Set permissions
sudo chown -R www-data:www-data /var/www/html/
sudo chmod -R 755 /var/www/html/

# Create MySQL database and user for WordPress
sudo mysql -u root -p <<EOF
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'wppassword';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
EOF

# Rename WordPress sample config file
sudo mv /var/www/html/wp-config-sample.php /var/www/html/wp-config.php

# Configure WordPress database settings
sudo sed -i 's/database_name_here/wordpress/' /var/www/html/wp-config.php
sudo sed -i 's/username_here/wpuser/' /var/www/html/wp-config.php
sudo sed -i 's/password_here/wppassword/' /var/www/html/wp-config.php

echo "WordPress installation completed. You can access it at http://your_server_ip_address/"
```

Replace `"password"` in the `mysql_secure_installation` command with your desired MySQL root password. 

Make sure to give execute permissions to the script using
chmod +x install_wordpress.sh

Then you can execute the script:
./install_wordpress.sh


