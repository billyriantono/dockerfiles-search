FROM php:7.0-apache
RUN apt-get update -y && apt-get install -y openssl zip unzip git libmcrypt-dev exif libpng-dev libjpeg62-turbo-dev cron
RUN docker-php-ext-configure gd --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install pdo pdo_mysql mbstring mcrypt exif gd zip
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require hirak/prestissimo
