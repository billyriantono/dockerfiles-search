FROM php:7.3.12-fpm-buster

RUN apt-get update && apt-get install -y sudo \
    nano \
    supervisor \
    git \
    zip \
    libzip-dev \
    unzip \
    openssl \
    procps \
    acl \
    zlib1g-dev \
    libxml2-dev \
    libpng-dev \
    wget \
    gdebi \
    gnupg \
    libpq-dev \
    librabbitmq-dev
    # Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer; \
    composer --version; \
    mkdir /var/www/.composer; \
    chown -R www-data /var/www/.composer
    # Install MySQL
RUN apt-get install -y default-mysql-client
    # Install extensions
RUN docker-php-ext-configure zip --with-libzip
RUN docker-php-ext-install pdo \
    pdo_mysql \
    bcmath \
    xml \
    gd \
    mbstring \
    soap \
    intl \
    posix \
    zip \
    mysqli \
    ftp
    # install ampq
RUN pecl install amqp; \
    docker-php-ext-enable amqp
    # Install xdebug
RUN pecl install xdebug; \
    docker-php-ext-enable xdebug; \
    echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "xdebug.idekey=\"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "xdebug.remote_port=9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
    # Configure php
COPY config/tzone.ini /usr/local/etc/php/conf.d/tzone.ini
COPY config/uploads.ini /usr/local/etc/php/conf.d/uploads.ini
