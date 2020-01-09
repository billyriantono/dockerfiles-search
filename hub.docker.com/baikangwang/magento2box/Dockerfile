FROM magento/magento2devbox-web

ENV USE_RABBITMQ 0
ENV USE_REDIS_FULL_PAGE_CACHE 0
ENV USE_REDIS_CACHE 0
ENV USE_REDIS_SESSIONS 0
ENV USE_VARNISH 0
ENV USE_ELASTICSEARCH 0
ENV MAGENTO_PUBLIC_KEY 9b2029dc87ca99ea05946f8cbde0dd1b
ENV MAGENTO_PRIVATE_KEY 69f6228b4d5591bf867238e09dd14c60
ENV MAGENTO_USE_SOURCES_IN_HOST 0
ENV CREATE_SYMLINK_EE 0
ENV HOST_CE_PATH ./shared/webroot
ENV EE_DIRNAME magento2ee
ENV MAGENTO_DOWNLOAD_SOURCES_COMPOSER 1
ENV MAGENTO_EDITION ce
ENV MAGENTO_VERSION 2.1.6
ENV MAGENTO_SAMPLE_DATA_INSTALL 1
ENV MAGENTO_DOWNLOAD_SOURCES_CLOUD 0

ENV MAGENTO_CRON_RUN 0
ENV MAGENTO_DI_COMPILE 0
ENV MAGENTO_GRUNT_COMPILE 0
ENV MAGENTO_STATIC_CONTENTS_DEPLOY 0
ENV MAGENTO_BACKEND_PATH admin
ENV MAGENTO_ADMIN_USER admin
ENV MAGENTO_ADMIN_PASSWORD admin123
ENV MAGENTO_STATE_PATH /home/magento2/state
ENV MAGENTO_ENABLE_SYNC_MARKER enable_sync
ENV USE_UNISON_SYNC 1
ENV MAGENTO_WARM_UP_STOREFRONT 0

COPY ./auth.json /home/magento2/.composer/
RUN su magento2 && m2init magento:install --no-interaction --webserver-home-port=80 \
    && rm -rf /var/www/magento2/vendor/* \
    && exit

COPY ./apache-default.conf /etc/apache2/sites-enabled/
COPY ./default-ssl.conf /etc/apache2/sites-enabled/
COPY ./cmg-dev.conf /home/magento2/magento2/
RUN cd /home/magento2/magento2/ \
    && su magento2 && openssl req -config cmg-dev.conf -new -x509 -sha256 -newkey rsa:2048 -nodes -keyout cmg-dev.key.pem -days 3650 -out cmg-dev.cert.pem \
    && exit \
    && cp cmg-dev.key.pem /etc/ssl/private/cmg-dev.key.pem \
    && cp cmg-dev.cert.pem /etc/ssl/certs/cmg-dev.cert.pem \
    && cd /

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
