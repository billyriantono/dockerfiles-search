FROM squeezely/phpbase:latest
RUN apt-get update && apt-get install -y php7.2-fpm

RUN ln -s /etc/php/7.2/mods-available/redis.ini /etc/php/7.2/fpm/conf.d/20-redis.ini
RUN ln -s /etc/php/7.2/mods-available/newrelic.ini /etc/php/7.2/fpm/conf.d/20-newrelic.ini
RUN mkdir -p /run/php
COPY opcache.ini /etc/php/7.2/mods-available/opcache.ini

RUN rm /etc/php/7.2/fpm/pool.d/www.conf
COPY www.conf /etc/php/7.2/fpm/pool.d/www.conf.base

COPY entrypoint.sh /usr/local/bin/entrypoint-fpm.sh
RUN ln -s usr/local/bin/entrypoint-fpm.sh / # backwards compat
ENTRYPOINT ["entrypoint-fpm.sh"]

CMD ["php-fpm7.2", "-F"]
