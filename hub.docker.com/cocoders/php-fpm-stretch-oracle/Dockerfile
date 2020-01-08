FROM php:7.3-fpm-stretch

RUN apt update && apt upgrade
RUN apt -y install git unzip wget zlib1g-dev libpq-dev libzip-dev libicu-dev wget gnupg iputils-ping vim

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main" | tee /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc |   apt-key add -
RUN apt update
RUN apt install -y postgresql-11 postgresql-client-11

RUN docker-php-ext-install intl zip pdo pdo_pgsql opcache pgsql sockets bcmath

# Oracle instantclient
RUN apt -y install libaio-dev
ENV LD_LIBRARY_PATH /usr/local/instantclient_18_3/

COPY ./oracle /tmp

RUN unzip /tmp/instantclient-basic-linux.x64-18.3.0.0.0dbru.zip -d /usr/local/
RUN unzip /tmp/instantclient-sdk-linux.x64-18.3.0.0.0dbru.zip -d /usr/local/
RUN unzip /tmp/instantclient-sqlplus-linux.x64-18.3.0.0.0dbru.zip -d /usr/local/
RUN ln -s /usr/local/instantclient_18_3 /usr/local/instantclient
RUN ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus

RUN docker-php-ext-configure oci8 --with-oci8=instantclient,/usr/local/instantclient
RUN docker-php-ext-install oci8

ADD php.ini /usr/local/etc/php/php.ini

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && php composer-setup.php && mv composer.phar /usr/local/bin/composer

WORKDIR /var/www/ava-bss-enrollment-api
