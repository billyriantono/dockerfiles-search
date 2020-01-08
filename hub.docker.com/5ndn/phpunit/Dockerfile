FROM php:7.0-cli
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        wget \
        libxml2-dev \
        php-soap \
        libpq-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install mysqli pdo pdo_mysql pdo_pgsql \
    && docker-php-ext-install -j$(nproc) soap

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

WORKDIR /temp

RUN wget https://phar.phpunit.de/phpunit-5.7.phar 
RUN chmod +x phpunit-5.7.phar
RUN mv phpunit-5.7.phar /usr/local/bin/phpunit

VOLUME /app

WORKDIR /app

ENTRYPOINT ["/usr/local/bin/phpunit"]
