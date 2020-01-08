FROM php:7.1-fpm

RUN apt-get update \
    && apt-get install -y nodejs zlib1g-dev nginx zip unzip libpng-dev

RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install opcache
RUN docker-php-ext-install zip
RUN docker-php-ext-install gd

RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN mv composer.phar /usr/local/bin/composer
RUN php -r "unlink('composer-setup.php');"
RUN mkdir /app
