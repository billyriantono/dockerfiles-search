FROM 2dotstwice/nginx-php71-starter

MAINTAINER Kristof Coomans "kristof@2dotstwice.be"
ENV REFRESHED_AT "2017-09-06 10:24:00"

# Pro hosting package nginx configuration
# Increase worker processes from 2 to 4.
RUN sed -i -e "s/worker_processes 2/worker_processes 4/g" /etc/nginx/nginx.conf

# Pro hosting package php-fpm configuration
ADD ./files/etc/php/fpm/pool.d/www.conf ${PHP_CONFIG_DIR}/fpm/pool.d/www.conf
