FROM bananabb/ubuntu-base:base.3.0.0
MAINTAINER BananaBb

# Install nginx & packages & php
RUN sudo apt-get update \
 && sudo DEBIAN_FRONTEND=noninteractive apt-get -qq install -y \
    nginx \
    supervisor \
    cron \
    libpcre3-dev \
    software-properties-common \
    php7.2-fpm \
    php7.2-common \
    php7.2-mbstring \
    php7.2-xmlrpc \
    php7.2-soap \
    php7.2-gd \
    php7.2-xml \
    php7.2-intl \
    php7.2-mysql \
    php7.2-cli \
    php7.2-zip \
    php7.2-curl

# Build Folder
RUN mkdir -p /var/www/public \ 
  /var/log/supervisor \
  /etc/nginx \
  /var/run/php/php7.2-fpm \
  /etc/php/conf.d

# Setup File
RUN sudo rm /etc/nginx/sites-available/default \
 && sudo cp /usr/share/nginx/html/index.html /var/www/public/

# File setting
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY Default /etc/nginx/sites-available/default
COPY installer composer-setup.php

# Setup Composer
RUN php composer-setup.php \
 && mv composer.phar /usr/local/bin/composer \
 && rm composer-setup.php

EXPOSE 80 443
CMD ["/usr/bin/supervisord"]