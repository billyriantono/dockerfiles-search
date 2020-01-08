FROM php:7.2-cli-buster
ENV DEBIAN_FRONTEND="noninteractive"
RUN apt-get update -yqq && apt-get upgrade -yqq
RUN apt-get install -yqq --no-install-recommends librdkafka-dev apt-utils libxml2-dev \
libfreetype6-dev libjpeg62-turbo-dev libpng-dev findutils make wget unzip gzip zlib1g-dev git wkhtmltopdf
RUN docker-php-ext-install zip pdo_mysql calendar dom json simplexml intl gd
RUN wget https://raw.githubusercontent.com/composer/getcomposer.org/76a7060ccb93902cd7576b67264ad91c8a2700e2/web/installer -O - -q | php -- --quiet && mv composer.phar /usr/local/bin/composer
RUN pecl update-channels && pecl install rdkafka-3.1.2 apcu && docker-php-ext-enable rdkafka apcu zip pdo_mysql calendar dom json simplexml intl gd

# OPCACHE
RUN docker-php-ext-install opcache && docker-php-ext-enable opcache

# XDEBUG
#RUN wget http://xdebug.org/files/xdebug-2.6.0.tgz
#RUN tar -xvzf xdebug-2.6.0.tgz
#RUN cd xdebug-2.6.0 && phpize && ./configure && make
#RUN cp xdebug-2.6.0/modules/xdebug.so /usr/local/lib/php/extensions/no-debug-non-zts-20160303
#RUN echo 'zend_extension = /usr/local/lib/php/extensions/no-debug-non-zts-20160303/xdebug.so' > /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN docker-php-ext-enable xdebug

COPY opcache_jenkins.ini $PHP_INI_DIR/conf.d/opcache_jenkins.ini
