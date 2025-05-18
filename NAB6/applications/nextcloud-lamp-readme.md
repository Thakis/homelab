## work in progress
[Nextcloud All-In-One installieren - Einfacher geht’s nicht!](https://www.youtube.com/watch?v=h5l2y00yeOY&list=PLRcp6YbTf6Qk3pIZnrKBTEJ8lQl5NZujz&index=6)

# updating 
apt update && apt upgrade -y

# Installing apache
apt install apache2 -y

# Install PHP 8.3 
apt install software-properties-common
add-apt-repository ppa:ondrej/php
apt update

# Install PHP 8.3 & Moduls
apt install php8.3 libapache2-mod-php8.3 php8.3-zip php8.3-xml php8.3-mbstring php8.3-gd php8.3-curl php8.3-imagick libmagickcore-6.q16-6-extra php8.3-intl php8.3-bcmath php8.3-gmp php8.3-cli php8.3-mysql php8.3-zip php8.3-gd  php8.3-mbstring php8.3-curl php8.3-xml php-pear unzip nano php8.3-apcu redis-server ufw php8.3-redis php8.3-smbclient php8.3-ldap php8.3-bz2 php8.3-sqlite3 

# adjust PHP.ini file
nano /etc/php/8.3/apache2/php.ini

memory_limit = 4096M
upload_max_filesize = 20G
post_max_size = 20G
date.timezone = Europe/Berlin
output_buffering = Off

opcache.enable=1
opcache.enable_cli=1
opcache.interned_strings_buffer=8
opcache.max_accelerated_files=10000
opcache.memory_consumption=128
opcache.save_comments=1
opcache.revalidate_freq=1

# Install Databse Server
apt install mariadb-server

# Maria DB Server Konfiguration
mysql_secure_installation

# open SQL dialoge
mysql

# create database calles nextcloud
CREATE DATABASE nextcloud; 

# create database user with password
CREATE USER 'nextclouduser'@'localhost' IDENTIFIED BY 'password_here';

#grant accesss to databse
GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextclouduser'@'localhost';

#save changes and exit
FLUSH PRIVILEGES;
EXIT;

# Download lastest nextcloud version
cd /tmp && wget https://download.nextcloud.com/server/releases/latest.zip
unzip latest.zip
mv nextcloud /var/www/

#create new conf
nano /etc/apache2/sites-available/nextcloud.conf

<VirtualHost *:80>
     ServerAdmin master@domain.com
     DocumentRoot /var/www/nextcloud/
     ServerName 

     <Directory /var/www/nextcloud/>
        Options +FollowSymlinks
        AllowOverride All
        Require all granted
          <IfModule mod_dav.c>
            Dav off
          </IfModule>
        SetEnv HOME /var/www/nextcloud
        SetEnv HTTP_HOME /var/www/nextcloud
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
 
# Enable the NextCloud and Rewrite Module

a2ensite nextcloud.conf
a2enmod rewrite
a2enmod headers
a2enmod env
a2enmod dir
a2enmod mime

# restart apache
service apache2 restart

# prepare data folder
mkdir /home/data/
chown -R www-data:www-data /home/data/

chown -R www-data:www-data /var/www/nextcloud/
chmod -R 755 /var/www/nextcloud/

---

[Installation von Nextcloud 30 I Teil 2/2 - Fehlerbehebung und Optimierung](https://www.youtube.com/watch?v=L2KAoCKZ7Iw)


1.
nano /var/www/nextcloud/config/config.php

'overwrite.cli.url' => 'https://192.168.178.207/nextcloud', 
'overwriteprotocol' => 'https',


2. 
crontab -u www-data -e

*/5 * * * * /usr/bin/php -f /var/www/nextcloud/cron.php

sudo chown -R www-data:www-data /var/www/nextcloud
sudo chmod +x /var/www/nextcloud/cron.php



3. 
nano /etc/php/8.3/cli/conf.d/20-apcu.ini

apc.enable_cli=1

service apache2 restart


4.
cd /var/www/nextcloud

sudo -u www-data php occ maintenance:repair --include-expensive

sudo -u www-data php occ db:add-missing-indices


5.
nano /var/www/nextcloud/config/config.php

'filelocking.enabled' => 'true',
'maintenance_window_start' => '1', 
'memcache.local' => '\OC\Memcache\APCu', 
'memcache.locking' => '\OC\Memcache\Redis', 
'redis' => array( 
'host' => 'localhost', 
'port' => 6379, 
),





6.
nano /var/www/nextcloud/config/config.php

"default_language" => "de", 
"default_locale" => "de", 
'default_phone_region' => 'DE',


---

 [Nextcloud Top 5 Security Essentials - So sicherst du deinen Nextcloud Server ab!](https://www.youtube.com/watch?v=0-hxlvR6f9g)

 #### Nextcloud Top 5 Security Essentials ####

#### Fail2Ban ####

## install fail2ban ##
apt install fail2ban

## create fail2ban filter ##
nano /etc/fail2ban/filter.d/nextcloud.conf

[Definition]
_groupsre = (?:(?:,?\s*"\w+":(?:"[^"]+"|\w+))*)
failregex = ^\{%(_groupsre)s,?\s*"remoteAddr":"<HOST>"%(_groupsre)s,?\s*"message":"Login failed:
            ^\{%(_groupsre)s,?\s*"remoteAddr":"<HOST>"%(_groupsre)s,?\s*"message":"Trusted domain error.
datepattern = ,?\s*"time"\s*:\s*"%%Y-%%m-%%d[T ]%%H:%%M:%%S(%%z)?"

## create fail2ban jail ##
nano /etc/fail2ban/jail.d/nextcloud.local

[nextcloud]
backend = auto
enabled = true
port = 80,443
protocol = tcp
filter = nextcloud
maxretry = 5
bantime = 86400
findtime = 43200
logpath = /home/data/nextcloud.log

## restart fail2ban ##
service fail2ban restart

## check status ##
fail2ban-client status nextcloud

##unban ip ##
fail2ban-client set nextcloud unbanip <ipadress>



#### Auto Logout ####

nano /var/www/nextcloud/config/config.php

'remember_login_cookie_lifetime' => 1296000,
'session_lifetime' => 1800,
'session_keepalive' => false,
'auto_logout' => true,


#### AntiVirus for Files ####

## Pakete installieren ##
apt install clamav clamav-freshclam clamav-daemon -y

## Stoppen Sie ClamAV und aktualisieren Sie die Virendatenbanken ##

service clamav-freshclam stop
freshclam
service clamav-freshclam start

## Passen Sie die clamav Konfiguration an, um größere Dateien(50MB) und Container-Dateien mit bis zu 25 Unterverzeichnissen scannen zu können ##

cp /etc/clamav/clamd.conf /etc/clamav/clamd.conf.bak
sed -i "s/MaxFileSize.*/MaxFileSize 50M/" /etc/clamav/clamd.conf
sed -i "s/MaxDirectoryRecursion.*/MaxDirectoryRecursion 25/" /etc/clamav/clamd.conf
sed -i "s/PCREMaxFileSize.*/PCREMaxFileSize 50M/" /etc/clamav/clamd.conf
sed -i "s/StreamMaxLength.*/StreamMaxLength 50M/" /etc/clamav/clamd.conf

## Im Anschluss daran werden die ClamAV relevanten Dienste neu gestartet ##
service clamav-freshclam restart && service clamav-daemon restart