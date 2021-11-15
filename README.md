# LAMP STACK
Cloud storage build within Microsoft Azure, providing storage and webapplication.

## Installation

Configure a new Azure Virtual Machine and create an SSH private key to connect to your VM.

```bash
ssh -i C:\..\..[yougavethisaname]_key.pem azureuser@127.0.0.1
```

## Usage

```python
Installing updates
$sudo apt-get update && sudo apt-get upgrade -y

# Installeren LAMP stack [Linux, Apache, MySQL, dbserver, PHP]
$ sudo apt-get install apache2
$ sudo systemctl status apache2

# MySQL
$ sudo apt-get install mysql-server
$ sudo mysql_secure_installation

# Edit MySQL database
$ sudo mysql

##CHECK attended user

Mysql> Select user, authentication_string FROM mysql.user;

##Secure root with authentication string>
Mysql> ALTER USER 'root'@'localhost' IDENTIFIES with mysql_native_password BY 'STRONG_PASSWORD';

$SHOW DATABASES;

#Install PHP [atleast 7.4]

$ sudo add-apt-repository ppa:ondrej/php
$ sudo add-apt-repository universe (may be <and I quote> already available for all sources.)

# install PHP, apache MySQL db+ dependecies for Wordpress and Nextcloud.

$ sudo apt-get install php7.4 libapache2-mod-php7.4 php7.4-mysql php7.4-common php7.4-gd php7.4-mbstring php7.4-fpm php7.4-json php7.4 php7.4-xml php7.4-xmlrpc php7.4-intl php7.4-curl php7.4-zip php7.4-imagick 

# Some modules may not be active

$ sudo a2emod proxy_fcgi setenvif
$ sudo a2enconf php7.4-fpm

>>restart Apache

$sudo systemctl restart apache2
##Create PHP page to see if the installation was succesfull

$ sudo vim /var/www/html/info.php

```PHP
<?php
  phpinfo();
?> 
```PHP

# Securing Apache certificate X openSSL (randomizing certificate)

$ openssl rand-writerand .rnd
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout 
/etc/ssl/private/562738-key.key -out /etc/ssl/certs/562738-cert.crt 

# Setting up SSL parameters

$ sudo vim /etc/apache2/conf-available/ssl-params.conf

## Configuration

 SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AE256+EECDH:AES256+EDH
 SSLProtocol All -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
 SSLHonorCipherOrder On
 Header always set X-Frame-Options DENY
 Header always set X-Content-Type-Options nosniff
 SSLCompression off
 SSLUseStapling on
 SSLStaplingCache "shmcb:logs/stapling-cache(150000)"
 SSLSessionTickets Off
 
# SSL installation, configuration (backup)
$ sudo cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/defaultssl.conf.bak

# EDIT CONFIGURATION
$ sudo vim /etc/apache2/sites-available/default-ssl.conf

ServerAdmin [mail]
Servername [intern IP]

# Redirect http to https
 \\People should automatically be redirected to https instead of http]

$ sudo vim /etc/apache2/sites-available/000-default.conf
ADD >>>>> Redirect "/" "https://IP/"

#### Setting up firewall
$ sudo ufw allow 'Apache Full'
$ sudo ufw allow oPENssh

####Enable firewall
$ sudo ufw enable

####Check with
$ sudo ufw status

# Enable SSL with

$ sudo a2enmod ssl 
$ sudo a2enmod headers 
$ sudo a2enmod rewrite 
$ sudo a2enconf ssl-params 
$ sudo a2ensite default-ssl 

restart apache2

$ sudo systemctl restart apache2
checksum

$ sudo apache2ctl configtest

# returns 'Syntax OK'












````

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.
