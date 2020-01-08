FROM php:7.2-fpm

ADD files/docker-php-pecl-install /usr/local/bin
ADD files/php.ini /usr/local/etc/php/conf.d/my-php.ini

RUN apt-get update && \
    apt-get install -y zlib1g-dev libicu-dev g++ libxml2-dev zip unzip curl git libpq-dev

RUN docker-php-ext-configure intl && \
    docker-php-ext-install intl mbstring pdo pdo_mysql pgsql pdo_pgsql bcmath soap zip opcache

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/bin --filename=composer && \
    php -r "unlink('composer-setup.php');"
