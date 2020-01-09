# Php fpm with alpine linux
FROM php:7.3-fpm-alpine AS setup

# Run 3 commands in one build layer.
# 1 - update package index
# 2 - add zlib-dev (required by php zip extension)
# 3 - add libzip-dev (required by php zip extension)
RUN apk update; \
    apk add zlib-dev; \
    apk add libzip-dev;

# Install zip extension
RUN docker-php-ext-install zip

# Use the default development configuration
RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

# Register the COMPOSER_HOME environment variable
ENV COMPOSER_HOME /composer

# Allow composer to execute scripts as super user to remove warnings
ENV COMPOSER_ALLOW_SUPERUSER 1

# Add global binary directory to PATH and make sure to re-export it
ENV PATH /composer/vendor/bin:$PATH

# Add composer from composer official image
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Install prestissimo to speed up installations
RUN composer global require hirak/prestissimo

# Install laravel cli
RUN composer global require laravel/installer

# Make a volume to share project root
VOLUME [ "/var/www" ]
WORKDIR /var/www

# Expose fpm default port
EXPOSE 9000
