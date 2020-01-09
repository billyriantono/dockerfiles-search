FROM squeezely/phpbase:latest
RUN ln -s /etc/php/7.2/mods-available/redis.ini /etc/php/7.2/cli/conf.d/20-redis.ini
RUN ln -sf /etc/php/7.2/mods-available/newrelic.ini /etc/php/7.2/cli/conf.d/20-newrelic.ini

COPY opcache.ini /etc/php/7.2/mods-available/opcache.ini
COPY php.ini /etc/php/7.2/cli/php.ini

CMD ["php", "-a"]
