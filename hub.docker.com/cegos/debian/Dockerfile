FROM php:5.6-apache

# Disable user prompts
ENV DEBIAN_FRONTEND noninteractive
		
RUN apt-get update && apt-get install -qy --no-install-recommends \
        git\
        wget \
        mysql-server \
        mysql-client \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libicu-dev \

    && docker-php-ext-install -j$(nproc) \
        iconv \
        mcrypt \
        gettext \
        intl \
        pdo_mysql \
        zip \
        gd \
        mysqli \

    && rm -rf /var/lib/apt/lists/*

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#Install PHPUnit
RUN wget https://phar.phpunit.de/phpunit.phar \
    && chmod +x phpunit.phar \
    && mv phpunit.phar /usr/local/bin/phpunit

# Set the default time zone
RUN touch $PHP_INI_DIR/php.ini && echo 'date.timezone = "Europe/Paris"' >> $PHP_INI_DIR/php.ini
