FROM php:7.4-rc-apache

ENV REDIS_VERSION "5.1.1"
ENV XDEBUG_VERSION "2.9.0"

ENV DEBIAN_FRONTEND "noninteractive"

RUN apt-get update && apt-get install -y \
        gettext \
        git \
        iproute2 \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmagickwand-dev \
        libpng-dev \
        libxml2-dev \
        mc \
        nano \
        redis-tools \
        zlib1g-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN docker-php-ext-install -j4 calendar dom exif iconv pdo_mysql soap \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j4 gd

RUN pecl install xdebug-$XDEBUG_VERSION \
	&& docker-php-ext-enable xdebug \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && pecl install redis-$REDIS_VERSION \
    && docker-php-ext-enable redis \
    && pecl install lzf \
    && docker-php-ext-enable lzf

RUN git clone --recursive --depth=1 https://github.com/kjdev/php-ext-lz4.git \
 && cd php-ext-lz4 \
 && phpize \
 && ./configure \
 && make -j8 \
 && make install

RUN echo "extension=lz4.so" > /usr/local/etc/php/conf.d/docker-php-ext-lz4.ini

RUN git clone --recursive --depth=1 https://github.com/kjdev/php-ext-snappy.git \
 && cd php-ext-snappy \
 && phpize \
 && ./configure \
 && make -j8 \
 && make install

RUN echo "extension=snappy.so" > /usr/local/etc/php/conf.d/docker-php-ext-snappy.ini

RUN git clone --recursive --depth=1 https://github.com/kjdev/php-ext-brotli.git \
 && cd php-ext-brotli \
 && phpize \
 && ./configure \
 && make -j8 \
 && make install

RUN echo "extension=brotli.so" > /usr/local/etc/php/conf.d/docker-php-ext-brotli.ini

RUN a2enmod rewrite headers
