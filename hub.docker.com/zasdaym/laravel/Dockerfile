# Composer stage
FROM composer:1.8.4 as composer

# Build argument to define source code location
ARG SRC="."

# Copy source code to /app (default WORKDIR)
COPY $SRC .

# Run composer installation
RUN composer global require hirak/prestissimo \
    && composer install --no-interaction --no-dev --no-ansi --optimize-autoloader

# Final stage
FROM php:7.3-apache

# Build argument to define source code location
ARG SRC="."

# Package list, use ENV because multiline support
ENV PKG \
    libpq-dev \
    libpng-dev

# Copy results from composer to default workdir
COPY --from=composer /app .

# Copy custom virtualhost conf
COPY vhost.conf /etc/apache2/sites-available/000-default.conf

# Install packages, php extensions, php.ini configuration
RUN apt-get update && apt-get install -y $PKG && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install -j$(nproc) pdo_pgsql \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-install -j$(nproc) opcache \
    && mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
    && a2enmod rewrite \
    && chown -R www-data:www-data .
