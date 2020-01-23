FROM php:5.5-fpm

MAINTAINER Support QUABLE <letuananha3@gmail.com>

WORKDIR /var/www

RUN apt-get update
RUN apt-get install -y  ruby-full
RUN apt-get install -y  openjdk-7-jre --fix-missing
RUN apt-get install -y  ant
RUN apt-get install -y  imagemagick
RUN apt-get install -y  php5-imagick
RUN apt-get install -y  exiftool
RUN apt-get install -y  mysql-client

RUN apt-get install -y  node
RUN apt-get install -y  npm
RUN npm install forever -g

# COPY ["etc/apt/sources.list", "/etc/apt/sources.list"]
COPY php.ini /usr/local/etc/php/

RUN apt-get update --fix-missing
RUN apt-get install -y python-software-properties
RUN apt-get install -y libpq-dev libmemcached-dev libmagickwand-dev libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng12-dev libssl-dev libsasl2-dev zlib1g-dev libssl-doc

### For media management
RUN docker-php-ext-configure gd '--with-freetype-dir=/usr/include/' '--with-jpeg-dir=/usr/include/'

### Various
### Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install bcmath
RUN docker-php-ext-enable bcmath

RUN docker-php-ext-install iconv mcrypt gd pdo_mysql mbstring

RUN pecl install imagick
RUN docker-php-ext-enable imagick

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

RUN docker-php-ext-install pdo pdo_mysql

RUN apt-get update && apt-get install -y \
    curl \
    unzip \
    vim \
    wget

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Set timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN "date"

RUN usermod -u 1000 www-data

EXPOSE 9000
CMD ["php-fpm"]