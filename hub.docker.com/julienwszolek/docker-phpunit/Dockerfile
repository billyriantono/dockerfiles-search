FROM php:7.1

RUN echo "mysql-server mysql-server/root_password password secret" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password secret" | debconf-set-selections

RUN apt-get update -yqq

RUN apt-get install git zip libpng-dev wget -yqq

RUN wget https://phar.phpunit.de/phpunit-5.7.phar
RUN chmod +x phpunit-5.7.phar
RUN mv phpunit-5.7.phar /usr/local/bin/phpunit

RUN apt-get -y update \
    && apt-get install -y libicu-dev\
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl

RUN docker-php-ext-install pdo_mysql gd bcmath

RUN echo “date.timezone = Europe/Paris” > /usr/local/etc/php/php.ini
RUN echo “memory_limit = 1024M” >> /usr/local/etc/php/php.ini
RUN echo “intl.default_locale = ‘fr’” >> /usr/local/etc/php/php.ini

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
