FROM composer as composer
COPY composer.json /app
RUN composer install --ignore-platform-reqs --no-scripts

FROM php:5.6-apache

RUN dpkg-divert --local --rename --add /sbin/initctl && ln -sf /bin/true /sbin/initctl

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y apt-utils libpq-dev libxml2-dev \
        libicu-dev libmcrypt-dev zlib1g-dev libmemcached-dev \
        libmemcached11 locales \
    && a2enmod rewrite

RUN pecl install xdebug-2.5.5 mcrypt-1.0.1 memcached-2.2.0 \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-configure intl

RUN docker-php-ext-install -j$(nproc)\
        ctype dom iconv intl json opcache mbstring pdo pdo_mysql pdo_pgsql \
        session simplexml tokenizer xml zip

# RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
#     && echo 'error_reporting = E_ALL' >> /usr/local/etc/php/conf.d/php-error-reporting.conf \
#     && echo 'display_errors = On' >> /usr/local/etc/php/conf.d/php-error-reporting.conf

RUN echo 'error_reporting = E_ALL' >> /usr/local/etc/php/conf.d/php-error-reporting.conf \
    && echo 'display_errors = On' >> /usr/local/etc/php/conf.d/php-error-reporting.conf

RUN touch /usr/local/etc/php/conf.d/php.ini

RUN echo "short_open_tag = Off/" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "short_open_tag = Off" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "display_errors = On" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "display_errors = On" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/php.ini

ADD 000-default.conf /etc/apache2/sites-available/000-default.conf

RUN rm -rf /var/lib/apt/lists/* \
    && apt-get clean

ADD log /var/www/html/log
ADD app /var/www/html/app
ADD public /var/www/html/public

EXPOSE 80

RUN chown -R www-data:www-data /var/www/html/log

WORKDIR /var/www/html
COPY --from=composer /app/vendor /var/www/html/vendor
