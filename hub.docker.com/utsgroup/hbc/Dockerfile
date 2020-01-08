FROM php:7.1-fpm

MAINTAINER camohob <v.samonov@mail.ru>

ENV HBC_ENV dev
VOLUME /app
VOLUME /app/vendor
VOLUME /tmp/.ssh

COPY conf/php-log.conf /usr/local/etc/php-fpm.d/zz-log.conf
COPY conf/php-$HBC_ENV.ini /usr/local/etc/php/conf.d/php.ini

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils git
RUN apt-get install -y unzip libicu-dev libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev
RUN docker-php-ext-install pdo pdo_mysql
RUN pecl install -o mailparse && docker-php-ext-enable mailparse
RUN docker-php-ext-install -j$(nproc) iconv mcrypt
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && docker-php-ext-install -j$(nproc) gd
RUN apt-get install -y libssl-dev pkg-config
RUN pecl install -o mongodb-1.5.2 redis-4.0.0 && docker-php-ext-enable mongodb redis
RUN apt-get install -y libpq-dev && docker-php-ext-configure pgsql --with-pgsql=/usr/local/pgsql && docker-php-ext-install pdo_pgsql
RUN docker-php-ext-install intl bcmath sockets
RUN apt-get install -y libyaml-dev && pecl install -o yaml && docker-php-ext-enable yaml
RUN apt-get install -y librabbitmq-dev && pecl install amqp && docker-php-ext-enable amqp
#RUN docker-php-ext-install opcache

COPY conf/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
RUN pecl install -o xdebug
RUN apt-get install -y ssh

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#RUN chmod +x /usr/local/bin/composer

WORKDIR /app
RUN mkdir -p /app/var/cache /app/var/logs
RUN chown -R www-data:www-data /var/www
RUN echo "alias sf='php bin/console'" >> /etc/bash.bashrc

RUN usermod -u 1000 www-data
USER www-data
CMD cp -R /tmp/.ssh /var/www/.ssh && chown -R www-data:www-data /app /var/www/.ssh && chmod 600 /var/www/.ssh/id_rsa && php-fpm
#RUN mkdir -p /var/www/.ssh
