# Use a multi-stage build to add composer into this container
FROM composer:latest

# Installs a parallel processing plugin to improve composer performance, when we run composer install.
RUN composer global require hirak/prestissimo

# Now add the PHP build
FROM php:7.2-fpm-alpine3.8
LABEL maintainer="thejoshsmith"

# Installs required libraries for the PHP environment.
# As the Alpine Distro is barebones, we need to install compiling tools first. These are removed at the end to keep the build size down.
# We require imagemagick and imagemagick-dev, otherwise the delegates for jpeg and png cannot be found.
# https://github.com/docker-library/php/issues/105#issuecomment-278114879
RUN apk add --update --no-cache \
  autoconf \
  g++ \
  gnupg \
  icu-dev \
  make \
  pcre-dev \
  composer \
  dpkg \
  gettext \
  php7-intl \
  php7-soap \
  libxml2-dev \
  libtool \
  libzip-dev \
  zip \
  libpng\
  libjpeg-turbo\
  imagemagick\
  imagemagick-dev \
  mysql-client \
  postfix \
  freetype \
  freetype-dev \
  libpng-dev \
  libjpeg-turbo-dev \
  optipng \
  jpegoptim \
  gifsicle \
  $PHPIZE_DEPS \
  && pecl install xdebug-2.7.0 \
  && docker-php-ext-enable xdebug \
  && cp /usr/bin/envsubst /usr/local/bin/ \
  && export CFLAGS="$PHP_CFLAGS" CPPFLAGS="$PHP_CPPFLAGS" LDFLAGS="$PHP_LDFLAGS" \
  && docker-php-ext-configure intl \
  && docker-php-ext-configure zip --with-libzip \
  && docker-php-ext-install bcmath mysqli pdo_mysql intl zip xml soap \
	&& pecl install imagick \
	&& docker-php-ext-enable imagick \
  && docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ \
  && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
  && docker-php-ext-install -j${NPROC} gd \
  && apk add gnu-libiconv --update-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted \
	&& apk del autoconf g++ icu-dev libtool make pcre-dev freetype-dev libpng-dev libjpeg-turbo-dev gettext

# Fix for iconv: https://github.com/docker-library/php/issues/240
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php

# Use the default production configuration
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

# Copy the postfix configuration file
COPY postfix-main.cf /root/conf/postfix-main.cf

# Copy entrypoint script and make executable
COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["php-fpm"]