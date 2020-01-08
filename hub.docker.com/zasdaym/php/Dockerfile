FROM php:7.3-apache-buster

# Package dependency list
ENV PKG \
    apt-utils \
    libpq-dev \
    libpng-dev \
    libzip-dev \
    zip

# Copy custom virtualhost configuration
COPY apache/vhost.conf /etc/apache2/sites-available/000-default.conf

# Copy composer executable from composer image
COPY --from=composer:1.9.0 /usr/bin/composer /usr/bin/composer

# Install packages, php extensions, php.ini configuration
RUN apt-get update && apt-get install -y $PKG && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install gd \
    && docker-php-ext-install opcache \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install zip \
    && mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
    && a2enmod rewrite \
    && chown -R www-data:www-data /var/www/
