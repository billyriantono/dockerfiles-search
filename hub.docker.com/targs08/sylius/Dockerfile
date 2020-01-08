FROM composer AS build-php
COPY . /app
RUN cd /app && composer install -n --ignore-platform-reqs

FROM node AS build-node
COPY --from=build-php /app /app
RUN cd /app && \
    yarn install && \
    yarn build

FROM php:7.2-apache

ENV TIMEZONE "Europe/Moscow"
ENV SYMFONY_ENV "prod"
ENV ICU_URL http://download.icu-project.org/files/icu4c/62.1/icu4c-62_1-src.tgz

RUN apt-get update && apt-get install --no-install-recommends --assume-yes \
			libpng-dev \
	&& rm -rf /var/lib/apt/lists/* \
	&& curl -sS -o /usr/src/icu.tar.gz -L $ICU_URL \
	&& tar -zxf /usr/src/icu.tar.gz -C /usr/src/ \
    && cd /usr/src/icu/source \
    && ./configure --prefix=/usr/local \
    && make \
    && make install \
    && rm -fr /usr/src/icu

RUN docker-php-ext-enable opcache \
    && export PHP_CPPFLAGS="$PHP_CPPFLAGS -std=c++11" \
    && docker-php-ext-configure intl --with-icu-dir=/usr/local \
    && docker-php-ext-install -j$(nproc) \
        intl \
        exif \
        gd \
        pdo_mysql

RUN echo 'date.timezone = ${TIMEZONE}' > /usr/local/etc/php/conf.d/date.ini

COPY apache.conf /etc/apache2/sites-available/000-default.conf
COPY --from=build-node --chown=33:33 /app/web/assets /var/www/html/web/assets
COPY --from=build-php  --chown=33:33 /app /var/www/html

RUN mv behat.yml.dist behat.yml && \
    rm apache.conf yarn.lock gulpfile.babel.js package.json