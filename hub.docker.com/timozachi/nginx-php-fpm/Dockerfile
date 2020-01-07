FROM php:7.1-fpm-alpine

MAINTAINER Timóteo Zachi <zachi.timo@gmail.com>

WORKDIR /var/www

# Nginx and supervisor to start both processes (nginx and php-fpm)
RUN apk update && apk upgrade \
    && apk add --no-cache \
        nginx \
        supervisor

# Cleanup the default directories
RUN rm -rf /var/www \
    && mkdir /var/www \
    && chown -R www-data:www-data /var/lib/nginx \
    && chown -R www-data:www-data /var/www \
    && cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.orig \
    && mkdir /run/nginx \
    # Uncomment the listen lines, and change the connection to the sock file
    && sed -i \
        -e "s/;listen.owner = www-data/listen.owner = www-data/g" \
        -e "s/;listen.group = www-data/listen.group = www-data/g" \
        -e "s/listen = 127.0.0.1:9000/listen = \/run\/php7.1-fpm.sock/g" \
        /usr/local/etc/php-fpm.d/www.conf \
    # Install essential php libraries (mbstring and json already present)
    && docker-php-ext-install iconv \
    # Cleanup everything
    && rm -rf /tmp/* /var/cache/apk/*

# These two configuration files are required
COPY conf/nginx.conf /etc/nginx/nginx.conf
COPY conf/supervisord.conf /etc/supervisord.conf
COPY files/* /etc/nginx/

EXPOSE 80
EXPOSE 443

# Start supervisor
CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]
