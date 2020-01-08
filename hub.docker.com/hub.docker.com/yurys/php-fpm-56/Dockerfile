FROM php:5.6-fpm

MAINTAINER Yu Shi <tttptd@yandex.com>

# PHP7, GD, ImageMagick, GraphicsMagick, Memcached, MySQL, Opcache...

RUN apt-get update && apt-get install -y \
    imagemagick \
    graphicsmagick \
    libmemcached-dev \
    zip \
    unzip \
    curl \
    --no-install-recommends \
    && rm -r /var/lib/apt/lists/*

# GD
RUN buildRequirements="libpng12-dev libjpeg-dev libfreetype6-dev" \
    && apt-get update && apt-get install -y ${buildRequirements} \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/lib \
    && docker-php-ext-install gd \
    && apt-get purge -y ${buildRequirements} \
    && rm -rf /var/lib/apt/lists/*

# Imagick
RUN runtimeRequirements="libmagickwand-6.q16-dev --no-install-recommends" \
    && apt-get update && apt-get install -y ${runtimeRequirements} \
    && ln -s /usr/lib/x86_64-linux-gnu/ImageMagick-6.8.9/bin-Q16/MagickWand-config /usr/bin/ \
    && pecl install imagick-3.4.0RC6 \
    && echo "extension=imagick.so" > /usr/local/etc/php/conf.d/ext-imagick.ini \
    && rm -rf /var/lib/apt/lists/*

# Opcache
RUN docker-php-ext-install opcache

# Zip
RUN docker-php-ext-install zip

# Install extensions using the helper script provided by the base image
RUN docker-php-ext-install pdo_mysql

# Install Memcached for php 7
# RUN curl -L -o /tmp/memcached.tar.gz "https://github.com/php-memcached-dev/php-memcached/archive/php7.tar.gz" \
#     && mkdir -p /usr/src/php/ext/memcached \
#     && tar -C /usr/src/php/ext/memcached -zxvf /tmp/memcached.tar.gz --strip 1 \
#     && docker-php-ext-configure memcached \
#     && docker-php-ext-install memcached \
#     && rm /tmp/memcached.tar.gz

# Install xdebug
# RUN pecl install xdebug \
#     && docker-php-ext-enable xdebug

CMD ["php-fpm"]

EXPOSE 9000
