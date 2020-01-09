FROM php:7.1-fpm

ENV TERM xterm

RUN apt-get update && apt-get install -y sudo

RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -

RUN apt-get install -y \
    libpq-dev \
    libjpeg-dev \
    libpng12-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev \
    libicu-dev \
    nginx \
    nodejs \
    build-essential \
    git \
    zip \
    cron \
    --no-install-recommends

# configure gd library
RUN docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-jpeg-dir=/usr/lib \
    --with-freetype-dir=/usr/include/freetype2

# Install mongodb, xdebug
RUN pecl install mongodb

# Install extensions using the helper script provided by the base image
RUN docker-php-ext-install \
    mcrypt \
    pdo_mysql \
    pdo_pgsql \
    gd \
    zip \
    intl

# Install other tools
RUN apt-get install supervisor net-tools nano -y

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
RUN npm install -g yarn

RUN curl -o composer-setup.php --silent --show-error https://getcomposer.org/installer
RUN sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN export COMPOSER_ALLOW_SUPERUSER=1
RUN rm -rf composer-setup.php

RUN sudo apt-get -y install xfonts-base xfonts-75dpi fontconfig xvfb wkhtmltopdf && mkdir ~/src/wkhtmltopdf -p && cd ~/src/wkhtmltopdf

RUN ln -s /usr/bin/wkhtmltopdf.sh /usr/local/sbin/wkhtmltopdf

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN usermod -u 1000 www-data

COPY php.ini /usr/local/etc/php/conf.d
COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/default.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN usermod -u 1000 www-data
WORKDIR /var/www/app

# Default command
CMD ["/usr/bin/supervisord"]

EXPOSE 80 443
