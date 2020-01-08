FROM php:7.1-apache

# Install required packages (Debian based)
RUN apt update && apt install -y \
        gettext \
        unzip \
        libpq-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev

# Configure and install gettext extension
RUN docker-php-ext-install zip

# Configure and install gettext extension
RUN docker-php-ext-install gettext

# Configure and install gd extension
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd

# Configure and install postgres php extension
RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql 
RUN docker-php-ext-install pdo pdo_pgsql pgsql pdo_mysql

