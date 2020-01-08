FROM cbeier/php:latest

ENV WODBY_DIR_FILES /mnt/files
ENV WODBY_DIR_CONF /var/www/conf

RUN su -l www-data -c "composer global require drush/drush" && \
    su -l www-data -c "composer clear-cache" && \
    mv /usr/local/bin/actions.mk /usr/local/bin/php.mk && \
    mkdir -p $WODBY_DIR_FILES && \
    mkdir -p $WODBY_DIR_CONF && \
    chown -R www-data:www-data $WODBY_DIR_CONF

COPY templates/* /etc/gotpl/
COPY actions /usr/local/bin
COPY init/* /docker-entrypoint-init.d/