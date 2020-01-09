FROM php:7.3.10-fpm-stretch

RUN apt-get update && apt-get install -y git zip libzip-dev unzip \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    libicu-dev libxml2-dev libxslt-dev \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ \
    && docker-php-ext-configure xsl --with-xsl \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
    && docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-install zip gd intl xsl pdo_mysql bcmath opcache \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/html/

EXPOSE 9000

CMD ["php-fpm"]
