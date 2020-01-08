FROM php:7.1.33-fpm-stretch

RUN apt-get update && apt-get install -y nano \
    supervisor \
    git \
    unzip \
    openssl \
    procps \
    acl \
    zlib1g-dev \
    libxml2-dev \
    libpng-dev \
    libmcrypt-dev \
    wget \
    gdebi \
    gnupg \
    libpq-dev \
    librabbitmq-dev \
    libssl-dev
    # Install MySQL
RUN apt-get install -y default-mysql-client
    # Install extensions
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
    mcrypt \
    mysqli \
    ftp
    # Install Wkhtmltopdf
RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb; \
    gdebi --n wkhtmltox_0.12.5-1.stretch_amd64.deb; \
    rm wkhtmltox_0.12.5-1.stretch_amd64.deb; \
    mkdir /var/www/html/dispones; \
    mkdir /var/www/html/dispones/vendor; \
    mkdir /var/www/html/dispones/vendor/h4cc; \
    mkdir /var/www/html/dispones/vendor/h4cc/wkhtmltopdf-amd64; \
    mkdir /var/www/html/dispones/vendor/h4cc/wkhtmltoimage-amd64; \
    mkdir /var/www/html/dispones/vendor/h4cc/wkhtmltopdf-amd64/bin; \
    mkdir /var/www/html/dispones/vendor/h4cc/wkhtmltoimage-amd64/bin; \
    cp /usr/local/bin/wkhtmltopdf /var/www/html/dispones/vendor/h4cc/wkhtmltopdf-amd64/bin/wkhtmltopdf-amd64; \
    cp /usr/local/bin/wkhtmltoimage /var/www/html/dispones/vendor/h4cc/wkhtmltoimage-amd64/bin/wkhtmltoimage-amd64;
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
