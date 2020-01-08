FROM nextcloud:13.0.4-fpm

RUN usermod -u 82 www-data
RUN groupmod -g 82 www-data

COPY redis.config.php /usr/src/nextcloud/config/redis.config.php
