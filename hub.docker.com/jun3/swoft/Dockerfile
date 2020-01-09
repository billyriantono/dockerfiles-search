FROM php:7.1-alpine

MAINTAINER Jun <zhoujun3372@gmail.com>

RUN apk --update add wget \
	curl \
    git \
    build-base \
    libmemcached-dev \
    libmcrypt-dev \
    libxml2-dev \
    zlib-dev \
    autoconf \
    cyrus-sasl-dev \
    libgsasl-dev \
    supervisor \
    libpng-dev \
    libpng \
    tzdata \
    hiredis

# Timezone
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime


RUN curl -sS https://install.phpcomposer.com/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update --clean-backups


RUN docker-php-ext-install mysqli mbstring pdo pdo_mysql tokenizer xml zip

RUN pecl channel-update pecl.php.net

# Redis extension
RUN pecl install redis && docker-php-ext-enable redis && pecl clear-cache

RUN pecl install swoole && docker-php-ext-enable swoole

RUN pecl clear-cache

ADD . /var/www/swoft

WORKDIR /var/www/swoft

RUN composer install --no-dev && composer dump-autoload -o && composer clearcache

EXPOSE 80

CMD ["php", "/var/www/swoft/bin/swoft", "start"]
