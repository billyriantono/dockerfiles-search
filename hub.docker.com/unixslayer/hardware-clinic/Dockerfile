#
# PHP Dependencies
#
FROM composer as vendor

ENV COMPOSER_ALLOW_SUPERUSER=1

COPY composer.json composer.json
COPY composer.lock composer.lock

RUN composer global require hirak/prestissimo --no-plugins --no-scripts --no-suggest
RUN composer install --ignore-platform-reqs --prefer-dist --optimize-autoloader --no-suggest

#
# Application
#
FROM php:7.2-apache

MAINTAINER Piotr Zając <piotr.zajac@unixslayer.pl>

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

RUN apt-get update -y && \
    apt-get install -y \
    git \
    unzip \
    zlib1g-dev \
    libicu-dev \
    libxml2-dev \
    libmcrypt-dev \
    libxslt1-dev \
    mysql-client \
  && pecl install mcrypt-1.0.1 \
  && apt-get clean

RUN docker-php-ext-install \
  bcmath \
  intl \
  mbstring \
  soap \
  xsl \
  zip \
  opcache \
  pdo_mysql

RUN docker-php-ext-enable mcrypt

ENV LC_ALL=C.UTF-8 \
    LANG=C.UTF-8 \
    TINI_VERSION=v0.17.0 \
    SERVER_ENVIRONMENT="production" \
    SERVER_SERVICE="apache2" \
    SERVER_NAME="localhost" \
    SERVER_ADMIN="webmaster@localhost" \
    PHP_MEMORY_LIMIT="4G" \
    PHP_DATE_TIMEZONE="Europe/Warsaw" \
    PHP_OPCACHE_ENABLE=1 \
    PHP_OPCACHE_ENABLE_CLI=1 \
    PHP_OPCACHE_VALIDATE_TIMESTAMP=0 \
    COMPOSER_HOME="/var/www/.composer/" \
    COMPOSER_ALLOW_SUPERUSER=1 \
    APACHE_LOG_DIR="/var/log/apache2" \
    APACHE_DOCUMENT_ROOT="/var/www/html/public" \
    DATABASE_HOST=database \
    DATABASE_PORT=3306 \
    DATABASE_USER=clinic \
    DATABASE_NAME=clinic \
    DATABASE_PASS=hardwareclinic

WORKDIR /var/www/html

ADD docker/php/php.ini /usr/local/etc/conf.d/php.ini
ADD docker/apache2/sites-enabled/000-default.conf /etc/apache2/sites-enabled/000-default.conf
ADD docker/apache2/conf-enabled/* /etc/apache2/conf-enabled/
ADD docker/app/entrypoint.sh /usr/local/bin/entrypoint.sh
ADD docker/app/deploy.sh /usr/local/bin/deploy.sh
ADD docker/app/demo.sh /usr/local/bin/demo.sh

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN curl --location --output /sbin/tini https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini && chmod +x /sbin/tini

RUN a2enmod rewrite && \
    a2enmod status && \
    a2enmod headers && \
    a2enmod unique_id && \
    rm /etc/apache2/conf-enabled/other-vhosts-access-log.conf

RUN ln -sf /proc/self/fd/1 ${APACHE_LOG_DIR}/access.log && \
    ln -sf /proc/self/fd/1 ${APACHE_LOG_DIR}/error.log

COPY --chown=www-data:www-data . /var/www/html
COPY --from=vendor --chown=www-data:www-data /tmp /var/www/.composer
COPY --from=vendor --chown=www-data:www-data /app/vendor /var/www/html/vendor

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

CMD ["/usr/sbin/apache2ctl", "-DFOREGROUND"]
