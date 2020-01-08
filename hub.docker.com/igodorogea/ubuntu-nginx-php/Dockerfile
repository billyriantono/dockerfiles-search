FROM ubuntu:18.04

LABEL maintainer="Ivan Godorogea"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y gnupg tzdata \
    && echo "UTC" > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update \
    && apt-get install -y software-properties-common \
    && add-apt-repository -y ppa:ondrej/php \
    && apt-get -qq install --no-install-recommends --no-install-suggests -y \
        curl ca-certificates zip unzip git nano mc supervisor nginx imagemagick php-imagick \
        php7.1-fpm php7.1-cli php7.1-common php7.1-soap php7.1-xml php7.1-zip \
        php7.1-mbstring php7.1-bcmath php7.1-curl php7.1-gd php7.1-intl \
        php7.1-json php7.1-mysql php7.1-readline php7.1-tidy php7.1-xmlrpc \
        php7.1-xsl php7.1-yaml php7.1-xdebug php7.1-mcrypt \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf \
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log \
    && rm -rf /var/www/html/*

ADD files/etc/nginx/sites-available/default /etc/nginx/sites-available/default
ADD files/etc/php/7.1/fpm/php-fpm.conf /etc/php/7.1/fpm/php-fpm.conf
ADD files/etc/supervisor/conf.d/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Fix permisions broken by windows FS
RUN chmod -x /etc/nginx/sites-available/default \
             /etc/php/7.1/fpm/php-fpm.conf \
             /etc/supervisor/conf.d/supervisord.conf \
    && echo "php_admin_value[upload_max_filesize] = 100M" >> /etc/php/7.1/fpm/pool.d/www.conf \
    && echo "php_admin_value[post_max_size] = 100M" >> /etc/php/7.1/fpm/pool.d/www.conf \
    && echo "php_admin_value[max_input_vars] = 1500" >> /etc/php/7.1/fpm/pool.d/www.conf \
    && echo "php_admin_value[max_execution_time] = 240" >> /etc/php/7.1/fpm/pool.d/www.conf \
    && echo "php_admin_value[memory_limit] = 192M" >> /etc/php/7.1/fpm/pool.d/www.conf \
    && echo "php_admin_value[xdebug.max_nesting_level] = 500" >> /etc/php/7.1/fpm/pool.d/www.conf \
    && echo "<h3 style='text-align: center'>Nginx works</h3>" > /var/www/html/index.html \
    && echo "<?php phpinfo();" > /var/www/html/index.php

WORKDIR /var/www/html

CMD ["supervisord"]
