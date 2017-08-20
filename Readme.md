Install Apache/php 7/MySQL

# apt-get install apache2

# apt-get -y install mysql-server mysql-client

# mysql_secure_installation

# mysql -u root -p

# apt-get -y install php7.0 libapache2-mod-php7.0

# vi /var/www/html/info.php
<?php
phpinfo();
?>

# systemctl restart apache2

# http://172.104.51.72/info.php

# apt-cache search php7.0

# apt-get -y install php7.0-mysql php7.0-curl php7.0-gd php7.0-intl php-pear php-imagick php7.0-imap php7.0-mcrypt php-memcache  php7.0-pspell php7.0-recode php7.0-sqlite3 php7.0-tidy php7.0-xmlrpc php7.0-xsl php7.0-mbstring php-gettext

# systemctl restart apache2

# apt-get -y install php7.0-opcache php-apcu

# systemctl restart apache2

# sudo apt-get install curl

# curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh

# sudo bash nodesource_setup.sh

# apt-get install nodejs

Finally, install the build-essential package for npm:

# apt-get install build-essential

# sudo mkdir /var/www/html/nodejs

# sudo nano /var/www/html/nodejs/hello.js

!/usr/bin/env nodejs
var http = require('http');
http.createServer(function (request, response) {
   response.writeHead(200, {'Content-Type': 'text/plain'});
   response.end('Hello World! Node.js is working correctly.\n');
}).listen(8080);
console.log('Server running at http://127.0.0.1:8080/');

# sudo chmod 755 /var/www/html/nodejs/hello.js

# sudo npm install -g pm2

# sudo pm2 startup systemd

#  sudo pm2 start /var/www/html/nodejs/hello.js

# sudo a2enmod proxy
# sudo a2enmod proxy_http
	
# service apache2 restart

# vi /etc/apache2/sites-available/demohost.com.conf


<VirtualHost *:80>
   ServerName demohost.com

   ProxyRequests Off
   ProxyPreserveHost On
   ProxyVia Full
   <Proxy *>
      Require all granted
   </Proxy>

   <Location /nodejs>
      ProxyPass http://127.0.0.1:8080
      ProxyPassReverse http://127.0.0.1:8080
   </Location>

    <Directory "/var/www/html/nodejs">
    AllowOverride All
    </Directory>
</VirtualHost>

# cd /etc/apache2/sites-enabled/
# ln -s ../sites-available/demohost.com.conf .
# service apache2 restart

# sudo services apache2 restart