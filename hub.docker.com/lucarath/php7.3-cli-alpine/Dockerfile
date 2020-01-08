FROM php:7.3-cli-alpine

RUN apk update --no-cache
RUN apk add --no-cache $PHPIZE_DEPS openssl unzip libzip-dev icu-dev imagemagick-dev inkscape rsync openssh
RUN pecl install imagick apcu xdebug
RUN docker-php-ext-install pdo pdo_mysql zip
RUN docker-php-ext-enable imagick apcu zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer 

RUN curl -L https://deployer.org/deployer.phar > /usr/local/bin/deployer \
    && chmod +x /usr/local/bin/deployer

COPY "memory_limit.ini" "/usr/local/etc/php/conf.d/memory_limit.ini"
