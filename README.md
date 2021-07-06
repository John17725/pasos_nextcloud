# PASOS DE INSTALACION NEXTCLOUD 👇
---
- sudo apt update
- sudo apt install apache2 mariadb-server libapache2-mod-php7.4
- sudo apt install php7.4-gmp php7.4-bcmath php-imagick php7.4-xml php7.4-zip

---

# BD CONFIG
- CREATE DATABASE nextclouddb CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
- CREATE USER "donchuyusr"@"localhost" IDENTIFIED BY "root";
- GRANT ALL PRIVILEGES ON *.* TO "donchuyusr"@"localhost" WITH GRANT OPTION;
- FLUSH PRIVILEGES;

- sudo uf allow 'Apache Full'

# DESCARGA DE NEXTCLOUD
---
- /var/www
- sudo wget -c https://download.nextcloud.com/server/releases/nextcloud-21.0.3.zip
- sudo unzip nextcloud-21.0.3.zip
- sudo chown -R www-data.www-data nextcloud/

# APACHE WEB SERVER CONFIG 
- nano /etc/apache2/conf-available/nextcloud.conf

### Pegar el contenido del recuadro en el fichero
```
Alias /nextcloud "/var/www/nextcloud/" 

<Directory /var/www/nextcloud/>
  Options +FollowSymLinks
  AllowOverride All
  
  <IfModule mod_dav.c>
    Dav off
  </IfModule>
  SetEnv HOME /var/www/nextcloud
  SetEnv HTTP_HOME /var/www/nextcloud
</Directory> 
```
---
# CONFIGURACION DE APACHE

- a2enconf nextcloud
- a2enmod rewrite 
- a2enmod headers
- a2enmod env
- a2enmod dir
- a2enmod mime

# CONFIGURACION PHP 10-OPCACHE.ini > /etc/php/7.4/apache2/conf.d
### Pegar el contenido del recuadro en el fichero
```
opcache.enable=1
opcache.enable_cli=1
opcache.interned_strings_buffer=8
opcache.max_accelerated_files=10000
opcache.memory_consumption=128
opcache.save.commets=1
opcache.revalidate_freq=1
```

