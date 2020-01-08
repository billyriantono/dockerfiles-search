FROM php:7.3-apache

LABEL maintainer="Kodamera <dev@kodamera.se>"

# Extract the PHP source.
RUN docker-php-source extract

# Install libs.
RUN apt-get update \
    && apt-get install -y \
        git \
        libpng-dev \
        libpq-dev \
        mysql-client \
        unzip \
        wget \
        libzip-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
    && rm -rf /var/lib/apt/lists/*

# Install PHP extensions.
RUN docker-php-ext-install \
        opcache \
        pdo \
        pdo_mysql \
        zip

# Install GD.
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# Install xdebug.
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

# Install Blackfire.
RUN version=$(php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;") \
    && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/$version \
    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp \
    && mv /tmp/blackfire-*.so $(php -r "echo ini_get('extension_dir');")/blackfire.so \
    && printf "extension=blackfire.so\nblackfire.agent_socket=tcp://blackfire:8707\n" > $PHP_INI_DIR/conf.d/blackfire.ini

# Copy the development PHP config from the PHP source.
RUN cp /usr/src/php/php.ini-development /usr/local/etc/php/php.ini

# Delete the PHP source.
RUN docker-php-source delete

# Copy the PHP configuration.
COPY php/drupal.ini /usr/local/etc/php/conf.d/

# Copy the Apache configuration.
COPY apache/drupal.conf /etc/apache2/sites-available/000-default.conf

# Enable Apache mods.
RUN a2enmod rewrite

# Fix permissions.
RUN chown -R www-data:www-data /var/www

# Set working directory.
WORKDIR /var/www/html

# Install composer. This requires Docker 17.05.
COPY --from=composer:1 /usr/bin/composer /usr/bin/composer

# Speed up composer downloads.
USER www-data
RUN /usr/bin/composer global require hirak/prestissimo
USER root

# Add xdebug configuration.
COPY xdebug/xdebug.ini /usr/local/etc/php/conf.d/
