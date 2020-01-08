FROM netw0rkeu/nginx-php:1.0.0
MAINTAINER http://github.com/netw0rkeu

RUN apt-get install -y wget
RUN wget -P /tmp https://files.phpmyadmin.net/phpMyAdmin/4.4.12/phpMyAdmin-4.4.12-all-languages.tar.gz
RUN mkdir /usr/share/nginx/www/ && cd /usr/share/nginx/www/ && tar -xvf /tmp/phpMyAdmin-4.4.12-all-languages.tar.gz --strip 1
RUN rm /tmp/phpMyAdmin-4.4.12-all-languages.tar.gz
ADD config.inc.php /usr/share/nginx/www/config.inc.php
RUN chmod 0755 /usr/share/nginx/www/config.inc.php
