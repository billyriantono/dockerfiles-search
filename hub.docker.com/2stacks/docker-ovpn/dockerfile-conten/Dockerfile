FROM php:7.2.23-apache 

RUN apt-get -y update --fix-missing \
    && apt-get upgrade -y \
    # Install GD Image
    && apt install -y --no-install-recommends \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libicu-dev \
    libmcrypt-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    # Install PDO - Mysqli
    && docker-php-ext-install pdo pdo_mysql \
    && docker-php-ext-install mysqli && docker-php-ext-enable mysqli \
    # Install mcrypt
    && pecl install mcrypt-1.0.1 \
    && docker-php-ext-enable mcrypt \
    # Install intl
    && docker-php-ext-install -j$(nproc) intl \
    #Install Calendar
    && docker-php-ext-configure calendar && docker-php-ext-install calendar \
    # Enable htaceess rerite
    && a2enmod rewrite headers

