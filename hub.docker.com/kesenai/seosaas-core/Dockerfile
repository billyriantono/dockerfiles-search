FROM php:7.3-apache

WORKDIR /var/www/html

COPY core /var/www/html
COPY config/apache/000-default.conf /etc/apache2/sites-enabled

RUN apt-get update && apt-get install -y \
    gnupg2 \
    libpq-dev \
    libzip-dev \
    zlib1g-dev \
    && docker-php-ext-install pdo pdo_pgsql zip \
    && curl -sL https://deb.nodesource.com/setup_11.x | bash - \
    && apt-get install -y nodejs \
    && curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && chown -R www-data:www-data /var/www/html/var/log \
    && a2enmod rewrite \
    && npm install \
    && npm run build \
    && composer install \