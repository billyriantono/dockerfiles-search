FROM dylanlindgren/docker-laravel-phpfpm

MAINTAINER "Dylan Lindgren" <dylan.lindgren@gmail.com>

# Configure PHP-FPM
RUN sed -i '/^;clear_env = .*/aclear_env = no' /etc/php5/fpm/pool.d/www.conf

RUN mkdir -p /data
VOLUME ["/data"]

EXPOSE 9000

ENTRYPOINT ["/usr/sbin/php5-fpm", "-F"]
