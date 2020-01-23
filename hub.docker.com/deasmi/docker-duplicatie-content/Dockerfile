FROM php:7.3-fpm

# Enable Lib Sodium
RUN docker-php-ext-enable sodium
RUN docker-php-ext-install bcmath

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer