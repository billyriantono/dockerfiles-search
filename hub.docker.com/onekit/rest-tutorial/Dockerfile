FROM php:7.2.9-fpm
MAINTAINER Aliaksandr Harbunou "onekit@gmail.com"
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV ICU_RELEASE=62.1
ENV HOME /var/www/app
#php modules
RUN apt-get update && apt-get install -y \
    git \
    zip \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
	libicu-dev \
	libpq-dev \
	mysql-client && \
	docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql && \
    docker-php-ext-install pdo pdo_pgsql pgsql && \
    cd /tmp && curl -Ls http://download.icu-project.org/files/icu4c/$ICU_RELEASE/icu4c-$(echo $ICU_RELEASE | tr '.' '_')-src.tgz > icu4c-src.tgz && \
    cd /tmp && tar xzf icu4c-src.tgz && cd /tmp/icu/source && sed -i'' 's/define U_USING_ICU_NAMESPACE 0/define U_USING_ICU_NAMESPACE 1/g' common/unicode/uversion.h && ./configure && make && make install && rm -rf /tmp/icu /tmp/icu4c-src.tgz && \
	docker-php-ext-configure intl && \
	docker-php-ext-install intl && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install zip && \
    docker-php-ext-install exif && \
    pecl install apcu && \
    docker-php-ext-enable apcu && \
    pecl install mcrypt-1.0.1 && \
    docker-php-ext-enable mcrypt && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd
WORKDIR /var/www/app
#composer install
RUN curl -sS https://getcomposer.org/installer | php -- --filename=composer --install-dir=/usr/local/bin
