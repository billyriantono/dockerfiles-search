FROM php:7.3-rc-fpm-alpine

# RUN apt-get update \
#     && apt-get install -y \
#         git \
#         zip \
#         unzip \
#         libpng-dev \
#         libicu-dev \
#     && pecl install ds \
#     && pecl install redis-3.1.4 \
#     && pecl install xdebug-2.6.0 \
#     && docker-php-ext-enable \
#         ds \
#         redis \
#         xdebug \
#     && docker-php-ext-install \
#         bcmath \
#         gd \
#         intl \
#         opcache \
#         pdo_mysql \
#         zip \
#     && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
#     && composer global require "hirak/prestissimo:^0.3" \
#     && apt-get clean -y \
#     && apt-get autoclean -y \
#     && apt-get autoremove -y \
#     && rm -rf /var/lib/apt/lists/* /var/lib/log/* /tmp/* /var/tmp/*

WORKDIR /usr/local/app
