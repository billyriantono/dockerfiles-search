ARG PHP_VERSION=7.2
ARG ALPINE_VERSION=3.8

FROM php:${PHP_VERSION}-fpm-alpine${ALPINE_VERSION}

# Argumens. This build argumens have to be defined after of the base image, in other way, the parameters will be
# in blank.
# Defaults are assumed values of production.
ARG UID=1000
ARG GID=1000
ARG INSTALL_DEVLOPMENT_TOOLS=false
ARG TZ=UTC

LABEL maintainer="Victor Aguilar <victor.aguilar@ciencias.unam.mx>"

COPY ./symfony.ini /usr/local/etc/php/conf.d
COPY ./xsymfony.pool.conf /usr/local/etc/php-fpm.d/
COPY ./php.ini /usr/local/etc/php/php.ini

# Timezone
RUN apk add --no-cache tzdata
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

## User configuration
RUN apk add --no-cache shadow && \
    usermod -u ${UID} www-data && \
    groupmod -g ${GID} www-data && \
    apk del shadow

#####################################
# Extensions
#####################################

# Basic extensions
RUN docker-php-ext-install \
    pdo_mysql \
    mysqli

# zip
RUN apk add --update --no-cache libzip-dev && \
    docker-php-ext-install zip && \
    apk del libzip-dev

# opcache
RUN docker-php-ext-install opcache && \
    docker-php-ext-enable opcache

# apcu
RUN docker-php-source extract \
    && apk add --no-cache --virtual .phpize-deps-configure $PHPIZE_DEPS \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && apk del .phpize-deps-configure \
    && docker-php-source delete

# icu
RUN apk add --no-cache icu icu-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && apk del icu-dev

#####################################
# Development tools
#####################################

RUN if [ ${INSTALL_DEVLOPMENT_TOOLS} = true ]; then \
      apk add --no-cache php7-pecl-xdebug \
    ;fi

COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN if [ ${INSTALL_DEVLOPMENT_TOOLS} = false ]; then \
      rm /usr/local/etc/php/conf.d/xdebug.ini \
    ;fi

RUN if [ ${INSTALL_DEVLOPMENT_TOOLS} = true ]; then \
      php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
      php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    ;fi

RUN if [ ${INSTALL_DEVLOPMENT_TOOLS} = true ]; then \
      apk add --no-cache \
        git \
        openssh \
    ;fi

# In develop, the most of the time, we will enter to the container as www-data then it need to have prestisimo
# in its user directory.
USER www-data
RUN if [ ${INSTALL_DEVLOPMENT_TOOLS} = true ]; then \
      composer global require hirak/prestissimo \
  ;fi
USER root

CMD ["php-fpm"]

EXPOSE 9000
