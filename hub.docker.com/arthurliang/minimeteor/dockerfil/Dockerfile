FROM php:7.1-fpm

# install system extensions we need
RUN apt-get update && apt-get install -y \
    libpng-dev libpng++-dev libfreetype6-dev libjpeg62-turbo-dev  \
    libjpeg-dev libpq-dev zip wget git imagemagick \
    zlib1g-dev libicu-dev g++ libmagickwand-dev \
    fontconfig libfreetype6 libx11-6 libxcb1 libxext6 libxrender1 \
    xfonts-75dpi xfonts-base libssl-dev libssl1.1

RUN apt-get install -y -f libssl1.0-dev

RUN docker-php-ext-install gd pdo_pgsql intl bcmath

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

RUN php composer-setup.php && rm composer-setup.php && mv composer.phar /usr/local/bin/composer

RUN pecl install imagick

RUN docker-php-ext-enable imagick imagick.so

RUN composer global require "hirak/prestissimo:^0.3"

RUN wget http://archive.ubuntu.com/ubuntu/pool/main/libj/libjpeg-turbo/libjpeg-turbo8_1.4.2-0ubuntu3.1_amd64.deb
RUN dpkg -i libjpeg-turbo8_1.4.2-0ubuntu3.1_amd64.deb

RUN wget http://archive.ubuntu.com/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1.1_amd64.deb
RUN dpkg -i libpng12-0_1.2.54-1ubuntu1.1_amd64.deb

RUN wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.0.0_1.0.2g-1ubuntu4.13_amd64.deb
RUN dpkg -i libssl1.0.0_1.0.2g-1ubuntu4.13_amd64.deb

RUN wget https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.xenial_amd64.deb
RUN dpkg --install wkhtmltox_0.12.5-1.xenial_amd64.deb
