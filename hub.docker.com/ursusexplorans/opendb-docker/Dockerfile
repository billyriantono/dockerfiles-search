FROM php:5.6-apache

RUN apt-get update && apt-get upgrade -y
RUN apt-get install git -y

RUN apt-get install -y \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) gd mysql

#RUN git clone --branch RELEASE_1_6_2 https://github.com/pellcorp/opendb.git /var/www/html/
RUN git clone https://github.com/pellcorp/opendb.git /var/www/html/
ADD tables.sql /var/www/html/install/new/
RUN echo "<?php phpinfo(); ?>" >> /var/www/html/phpinfo.php
RUN echo "php_value date.timezone 'Europe/Berlin'" >> /var/www/html/.htaccess
RUN chmod ugo+w ./log ./include ./importcache ./itemcache ./upload ./httpcache
