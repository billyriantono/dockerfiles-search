FROM php:7.3.2-apache

RUN apt-get update && apt-get install -y \
wget \
libzip-dev \
zip \
git \
libxml2-dev \
mysql-client \
nano \
gnupg

# Activa modulos apache.
RUN a2enmod rewrite headers

# Agrega extenciones de docker para php.
RUN docker-php-ext-configure zip --with-libzip \
&& docker-php-ext-install zip \
&& docker-php-ext-install soap \
&& docker-php-ext-install intl \
&& docker-php-ext-install pdo_mysql

# Instalar nodejs.
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash && apt-get install nodejs -yq

# Instalar composer.
RUN curl -sS https://getcomposer.org/installer | php \
&& mv composer.phar /usr/local/bin/ \
&& ln -s /usr/local/bin/composer.phar /usr/local/bin/composer

# Permisos
RUN chown -R www-data:www-data /var/www/html

# Expone el puerto y deja apache corriendo por debajo.
EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND