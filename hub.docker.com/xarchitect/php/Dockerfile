FROM php:7.4-fpm

# Install modules
COPY php-fpm.conf /usr/local/etc/php-fpm.conf
RUN mkdir /var/log/php-fpm/
RUN mkdir -p /var/www/default

RUN apt-get update && apt-get install -y \
    libzip-dev \
	libmcrypt-dev  \
	libicu-dev \
    libssl-dev \
    libcurl4-openssl-dev \
    libonig-dev \
    zip \
    bzip2 \
	libpng-dev \
    git;

RUN docker-php-ext-install pdo_mysql;
RUN docker-php-ext-install zip;
RUN docker-php-ext-install gd;
RUN docker-php-ext-install intl;
RUN docker-php-ext-install mbstring;
RUN docker-php-ext-install mysqli;
RUN docker-php-ext-install opcache;

RUN pecl install apcu \
    && pecl install apcu_bc-1.0.3 \
    && docker-php-ext-enable apcu --ini-name 10-docker-php-ext-apcu.ini \
    && docker-php-ext-enable apc --ini-name 20-docker-php-ext-apc.ini

RUN apt-get install -y libxml2-dev;

RUN pecl install xdebug-2.8.0beta1; \
    docker-php-ext-enable xdebug; \
    echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "xdebug.show_exception_trace=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    echo "xdebug.show_error_trace=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini;

WORKDIR /var/www/default
CMD ["php-fpm"]
