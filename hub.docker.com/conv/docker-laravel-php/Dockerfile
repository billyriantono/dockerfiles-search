FROM php:7.2-fpm-stretch

ENV PATH="./vendor/bin:${PATH}" \
    NGINX_SERVER_NAME="_" \
    PHP_OPCACHE_VALIDATE_TIMESTAMPS="0" \
    PHP_OPCACHE_MAX_ACCELERATED_FILES="6000" \
    PHP_OPCACHE_MEMORY_CONSUMPTION="128"

RUN apt-get update \
    && apt-get -y --no-install-recommends install \
        procps \
        supervisor \
        sqlite3 \
        nginx \
        libzip-dev \
        zip \
        unzip \
        git \
        netcat \
        libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng-dev \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install mbstring pdo pdo_mysql zip opcache \
    && pecl install apcu xdebug-2.6.0alpha1 \
    && docker-php-ext-enable apcu xdebug \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd


COPY docker/php/php-fpm.d/docker.conf /usr/local/etc/php-fpm.d/zz-docker.conf
COPY docker/php/conf.d/*.ini /usr/local/etc/php/conf.d/
COPY docker/php/php.ini /usr/local/etc/php/php.ini

COPY docker/nginx/h5bp /etc/nginx/h5bp

COPY docker/supervisor/supervisord.conf /etc/supervisor/supervisord.conf
COPY docker/supervisor/conf.d/*.conf /etc/supervisor/conf.d-available/

COPY docker/run-app.sh /usr/local/bin/run-app
COPY docker/php/composer-installer.sh /usr/local/bin/composer-installer

ADD https://github.com/kelseyhightower/confd/releases/download/v0.11.0/confd-0.11.0-linux-amd64 /usr/local/bin/confd
COPY docker/confd/conf.d/ /etc/confd/conf.d/
COPY docker/confd/templates/ /etc/confd/templates/

RUN chmod +x /usr/local/bin/composer-installer \
    && chmod +x /usr/local/bin/confd \
    && chmod +x /usr/local/bin/run-app

RUN /usr/local/bin/composer-installer

RUN mv composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer

RUN composer --version


RUN chown www-data /var/www
USER www-data
RUN composer global require hirak/prestissimo
USER root

RUN chown -R www-data:www-data /var/www/html

EXPOSE 80

CMD ["/usr/local/bin/run-app"]
