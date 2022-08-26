# Laravel 8 on AWS and Aurora Mysql RDS 
Assignment

## Launch EC2 Instance ( Ubuntu ) 

##Elasti Ip Create 
Associate Elatic IP with EC2 Instance 

## Connect your EC2 
ssh -i ssh -i "test.pem" ubuntu@ec2-18-142-197-106.ap-southeast-1.compute.amazonaws.com 

$ sudo -i 

#apt update

## Installation nginx Web Service

#sudo apt install nginx 

#systemctl status nginx

#systemctl start nginx

#systemctl enable nginx

##Check Nginx Server From Browser
EC2 Instance Public IP (Elastic IP)

## PHP Installation
#apt-cache pkgnames | grep php7.4

#apt-get install php curl git unzip

#apt-get install php-pear php-fpm php-dev php-zip php-curl php-xmlrpc php-gd php-mysql php-mbstring php-xml libapache2-mod-php

 #php --version
 
## Composer Installation && Laravel install based on composer && permission 
#curl -sS https://getcomposer.org/installer | php 

#mv composer.phar /usr/bin/composer

#chmod +x /usr/bin/composer

#sudo chown -R www-data:www-data /var/www/

#sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;

#find /var/www -type f -exec sudo chmod 0664 {} \; 

#cd /var/www/html/

#composer create-project --prefer-dist laravel/laravel testing "8.*"

#cd /var/www/html/testing

#composer install

#cp .env.example .env

## Configuration File for nginx 

#vim /etc/nginx/sites-available/vhostlaravel.conf

  server {
  
     listen 80;
     
     listen [::]:80 ipv6only=on;

     # Log files for Debugging
     access_log /var/log/nginx/vhostlaravel-access.log;
     error_log /var/log/nginx/vhostlaravel-error.log;

     # Webroot Directory for Laravel project
     root /var/www/html/testing/public;
     index index.php index.html index.htm;

     # Your Domain Name
     server_name 13.250.100.133;

     location / {
             try_files $uri $uri/ /index.php?$query_string;
     }

     # PHP-FPM Configuration Nginx
     location ~ \.php$ {
             try_files $uri =404;
             fastcgi_split_path_info ^(.+\.php)(/.+)$;
             fastcgi_pass unix:/run/php/php7.4-fpm.sock;
             fastcgi_index index.php;
             fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
             include fastcgi_params;
     }
 }


#ln -s /etc/nginx/sites-available/vhostlaravel.conf /etc/nginx/sites-enabled/

#nginx -t

#systemctl reload nginx

#systemctl start php7.4-fpm 

#systemctl enable php7.4-fpm

#chmod -R 777 /var/www/html/testing/storage


## Security Group for nginx
Edit Inbound Rules
http 80     anywhere
https 443   anywhere 
ssh 22      anywhere

## Security Group for Database
Edit Inbound Rules
MySQL Aurora 3306   custom = VPC IP

#Connect Web Server and  Aurora DB

.env Config File

#cd /var/www/html/testing/

#vim .env 

DB_CONNECTION=mysql

DB_HOST=laraveldb.c9ar888l47xr.ap-southeast-1.rds.amazonaws.com   

DB_PORT=3306

DB_DATABASE=laraveldb

DB_USERNAME=root

DB_PASSWORD=*******

## Test Database Access from EC2 

#apt install mariadb-server

#systemctl status mariadb-server

#mysql -h (Aurora DB writer Endpoint) -u root -p 

mysql >

-------------------------------------------------------------------------------------







