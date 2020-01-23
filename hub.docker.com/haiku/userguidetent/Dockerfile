# Use PHP parent image
FROM php:7.2-apache


COPY . /app

# Set the working directory of the container to /app
COPY /Server/vhost.conf /etc/apache2/sites-available/000-default.conf
# Copy the current directory to the container

RUN chown -R www-data:www-data /app \
    && a2enmod rewrite \
    && service apache2 restart

# Install any necessary requirements to the container
RUN docker-php-ext-install mysqli

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer