FROM wordpress

MAINTAINER "Alexandru Berce" <alex@devaccent.ro>

RUN docker-php-ext-install mbstring pdo pdo_mysql \
    && docker-php-ext-install opcache

RUN touch /usr/local/etc/php/conf.d/memory-limit-php.ini \
    && echo "memory_limit = 2G;" >> /usr/local/etc/php/conf.d/memory-limit-php.ini

RUN touch /usr/local/etc/php/conf.d/max-execution-time-php.ini \
    && echo "max_execution_time = 600;" >> /usr/local/etc/php/conf.d/max-execution-time-php.ini

RUN touch /usr/local/etc/php/conf.d/uploads.ini \
    && echo "upload_max_filesize = 25M;" >> /usr/local/etc/php/conf.d/uploads.ini

RUN touch /usr/local/etc/php/conf.d/post-max-size.ini \
    && echo "post_max_size = 25M;" >> /usr/local/etc/php/conf.d/post-max-size.ini