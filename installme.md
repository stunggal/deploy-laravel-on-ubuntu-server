<!-- get update and upgrade -->
sudo apt-get update
sudo apt-get upgrade

<!-- install apache2 -->
apt install apache2

<!-- install mysql -->
sudo apt install mysql-server

<!-- install php -->
sudo apt install php libapache2-mod-php php-mysql

<!-- install phpmyadmin -->
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl

<!-- install git -->
sudo apt-get install git

<!-- install npm -->
sudo apt install nodejs
sudo apt install npm

<!-- install composer -->
sudo apt install curl
sudo apt install php-cli unzip
curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
HASH=`curl -sS https://composer.github.io/installer.sig`
echo $HASH
php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer

<!-- clone project -->
cd /var/www/html
sudo git clone https://<personal_token>@<directory_on_github>

<!-- load npm and composer -->
cd <name_of_project> 
npm i
composer i

<!-- set permission -->
sudo chgrp -R www-data /var/www/html/<name_of_project>/
sudo chmod -R 775 /var/www/html/<name_of_project>/storage

<!-- create a new virtual host -->
cd /etc/apache2/sites-available
sudo nano <name_of_project>.conf

<VirtualHost *:80>
   ServerName exampledomain.com
   ServerAdmin example@example.com
   DocumentRoot /var/www/html/<name_of_project>/public

   <Directory /var/www/html/<name_of_project>>
       AllowOverride All
   </Directory>
   ErrorLog ${APACHE_LOG_DIR}/error.log
   CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

<!-- disable the default configuration -->
sudo a2dissite 000-default.conf

<!-- enable the new virtual host -->
sudo a2ensite <name_of_project>

<!-- restart the Apache service -->
sudo a2enmod rewrite
sudo systemctl restart apache2