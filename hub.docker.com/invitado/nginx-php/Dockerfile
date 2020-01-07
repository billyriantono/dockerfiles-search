FROM php:7.0-fpm-alpine

# Install S6.
RUN apk add --update s6 && rm -rf /var/cache/apk/*

# Install nginx.
RUN apk add --update nginx && rm -rf /var/cache/apk/*

# Install needed PHP extensions.
RUN docker-php-ext-install pdo_mysql sockets opcache bcmath

# Install AMQP extension.
RUN echo "http://dl-4.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
    && apk add --update php7-amqp \
    && rm -rf /var/cache/apk/* \
    && mv /usr/lib/php7/modules/amqp.so /usr/local/lib/php/extensions/no-debug-non-zts-20151012/amqp.so \
    && mv /etc/php7/conf.d/40_amqp.ini /usr/local/etc/php/conf.d/40_amqp.ini

# Add logging for PHP.
RUN adduser -S www && mkdir -p /opt/log && mkfifo /opt/log/php-fpm && chown www /opt/log/php-fpm

# Add necessary configuration files.
RUN rm -rf /usr/local/etc/php-fpm.conf /usr/local/etc/php-fpm.d
COPY configuration/php-fpm.conf /usr/local/etc/
COPY configuration/nginx.conf /etc/nginx/

COPY s6 /opt/s6
RUN chmod -R 755 /opt/s6

# Add entrypoint script.
COPY entrypoint /opt/entrypoint
RUN chmod 755 /opt/entrypoint
CMD ["/opt/entrypoint"]

EXPOSE 80
