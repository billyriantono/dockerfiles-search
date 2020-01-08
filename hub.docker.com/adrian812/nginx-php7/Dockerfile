
FROM php:7.1.20-fpm-jessie

MAINTAINER adrian

# install iconv gd
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libmcrypt-dev \
        libmemcached-dev zlib1g-dev libssl-dev librabbitmq-dev nginx git cron unzip \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd pdo_mysql opcache bcmath zip

RUN pecl install memcached redis amqp

RUN docker-php-ext-enable opcache memcached redis pdo_mysql gd iconv amqp bcmath zip

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && chmod a+rx composer.phar \
    && mv composer.phar /usr/bin/composer

ADD resources/lib/libhiredis.so.0.13 /usr/lib/
ADD resources/extension/*.so /usr/local/lib/php/extensions/no-debug-non-zts-20160303/
RUN docker-php-ext-enable phpiredis loader_71 lua
RUN pecl clear-cache


ADD resources/conf/nginx.conf /etc/nginx/
ADD resources/conf/www.conf /etc/nginx/sites-enabled/
RUN rm /etc/nginx/sites-enabled/default

RUN apt-get install -y supervisor

ADD resources/conf/supervisord.conf /etc/
ADD resources/start.sh /
RUN chmod a+rx /start.sh

EXPOSE 80

CMD ["/start.sh"]
