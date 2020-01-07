FROM nginx:1.9

RUN apt-get update \
    && apt-get install -y \
        php5-fpm \
            php5-dev \
            php5-gd \
            php5-imagick \
            php5-mcrypt \
            php5-mysqlnd \
        wget \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean \
    && apt-get autoclean

RUN rm -f /etc/nginx/conf.d/default.conf \
    && mkdir -p /var/www/html \
    && rm -rf /var/www/html/* \
    && echo "<?php echo 'Hello World'; ?>" > /var/www/html/index.php \
    && chown -R www-data:www-data /var/www/html \
    && chmod -R 775 /var/www/html

VOLUME /var/www/html

RUN rm -f /etc/nginx/conf.d/*

COPY nginx/default.conf /etc/nginx/conf.d/default.conf
COPY php/docker.ini /etc/php5/mods-available/docker.ini
