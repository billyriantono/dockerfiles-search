FROM circleci/php:7.1-fpm-stretch-browsers-legacy

## Set defaults for php and add needed nginx sources
RUN echo "date.timezone = UTC" | sudo tee /usr/local/etc/php/conf.d/date.ini \
    && echo "memory_limit = -1" | sudo tee /usr/local/etc/php/conf.d/memory.ini \
    && echo "deb http://nginx.org/packages/debian/ stretch nginx" | sudo tee --append /etc/apt/sources.list \
    && echo "deb-src http://nginx.org/packages/debian/ stretch nginx" | sudo tee --append /etc/apt/sources.list \
    && sudo composer self-update

## Add nginx key signing for apt
RUN sudo wget https://nginx.org/keys/nginx_signing.key \
    && sudo apt-key add nginx_signing.key

## Add needed keys/deb source for nodejs and yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -

## Install node and php extensions
RUN sudo apt-get install -y nodejs autoconf libmemcached-dev libicu-dev libxml2-dev \
                            libfreetype6-dev libjpeg62-turbo-dev libpng-dev libjpeg-dev \
                            zlib1g-dev mysql-client xvfb chromium \
    && sudo pecl install memcached \
    && sudo docker-php-ext-enable memcached \
    && sudo docker-php-ext-configure intl \
    && sudo docker-php-ext-install intl \
    && sudo docker-php-ext-install zip \
    && sudo docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && sudo docker-php-ext-install gd \
    && sudo docker-php-ext-install soap \
    && sudo docker-php-ext-install mysqli \
    && sudo docker-php-ext-install pcntl \
    && sudo docker-php-ext-install pdo_mysql \
    && sudo docker-php-ext-install sockets

## This works here, add yarn deb
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

## Install Dependencies, once gem compass is removed, remove these packages: "ruby ruby-dev automake autogen libtool"
RUN sudo apt-get update && sudo apt-get install -y yarn ruby ruby-dev automake autogen libtool nginx supervisor

## Install compass/sass, consider compass deprecated, will be removed in the future
RUN sudo gem install --no-rdoc --no-ri sass -v 3.4.22
RUN sudo gem install --no-rdoc --no-ri compass

## Remove default nginx config
RUN sudo rm /etc/nginx/conf.d/default.conf

## Add default nginx config
ADD conf/default.nginx.conf /etc/nginx/conf.d/default.conf

## Add supervisord configs for nginx/php-fpm
ADD conf/nginx.supervisord.conf /etc/supervisor/conf.d/nginx.conf
ADD conf/php-fpm.supervisord.conf /etc/supervisor/conf.d/php-fpm.conf

## Cleanup
RUN sudo apt-get --purge remove automake autogen autoconf libtool \
    && sudo apt-get --purge autoremove

CMD sudo /usr/bin/supervisord -n -c /etc/supervisor/supervisord.conf
