FROM recesscreative/docker-wordpress:5.2.4_5.6

ENV WP_ROOT /usr/src/wordpress

COPY vhost.conf /etc/nginx/conf.d
COPY 99-custom.ini /usr/local/etc/php/conf.d
COPY wp-config.php /var/www/
COPY wp-settings.php /var/www/


COPY wp-config.php $WP_ROOT
RUN chown -R deployer:www-data $WP_ROOT \
    && chmod 644 $WP_ROOT/wp-config.php

RUN chown -R 82:82 /var/www/
