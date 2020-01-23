FROM php:5.6-apache

RUN apt-get update \ 
    && apt-get install -y vim \
    cron wget zip \
    mysql-client mydumper memcached \
    exif libpng-dev libjpeg-dev libkrb5-dev libxml2-dev libmcrypt-dev 
RUN docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install gd zip pdo_mysql

# Modify php.ini
WORKDIR /usr/local/etc/php/
RUN cp php.ini-production php.ini
RUN sed -i -e "s/upload_max_filesize\s*=\s*2M/upload_max_filesize = 1G/g" php.ini && \
    sed -i -e "s/post_max_size\s*=\s*8M/post_max_size = 1G/g" php.ini && \
    sed -i -e "s/max_execution_time\s*=\s*30/max_execution_time = 1000/g" php.ini && \
    sed -i -e "s/memory_limit\s*=\s*128M/memory_limit = 1G/g" php.ini


 WORKDIR /usr/local/etc/php/conf.d/
 RUN touch docker-php-custom.ini \
    && echo 'SecFilterEngine = Off' >> docker-php-custom.ini \
    && echo 'SecFilterScanPOST = Off' >> docker-php-custom.ini \
    && echo 'upload_max_filesize = 32M' >> docker-php-custom.ini \
    && echo 'post_max_size = 32M' >> docker-php-custom.ini \
    && echo 'max_execution_time = 1000' >> docker-php-custom.ini \
    && echo 'magic_quotes_* = Off' >> docker-php-custom.ini \
    && echo 'register_globals = Off' >> docker-php-custom.ini \
    && echo 'allow_url_fopen = On' >> docker-php-custom.ini \
    && echo 'safe_mode = Off' >> docker-php-custom.ini \
    && echo 'memory_limit = 1G' >> docker-php-custom.ini \
    && echo 'php_value short_open_tag = Off' >> docker-php-custom.ini 

# Enable apache mods.
RUN a2enmod php5 && \
    a2enmod rewrite




WORKDIR /var/www/html
RUN rm -rf * \
    && wget https://download.prestashop.com/download/releases/prestashop_1.6.1.18.zip \
    && unzip -q prestashop_1.6.1.18.zip \
    && chown -R www-data:www-data * \
    && mv prestashop/* . \
    && rm -rf prestashop

CMD ["apache2-foreground"]