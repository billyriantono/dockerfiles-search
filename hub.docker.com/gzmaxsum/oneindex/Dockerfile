FROM php:fpm-alpine

ENV ONEINDEX_CLIENT_ID 'ea2b36f6-b8ad-40be-bc0f-e5e4a4a7d4fa'
ENV ONEINDEX_CLIENT_SECRET 'EIVCx5ztMSxMsga18MQ7rmGf9EIP7zv6tfimb0Kp5Uc='
ENV ONEINDEX_REDIRECT_URI 'https://ju.tn/onedrive-login'
ENV ONEINDEX_DRIVE_ROOT ''
ENV ONEINDEX_CACHE_TYPE 'file'
ENV ONEINDEX_CACHE_EXPIRE_TIME 3600
ENV ONEINDEX_CACHE_REFRESH_TIME 600
ENV ONEINDEX_ROOT_PATH ''

WORKDIR /var/www/html
ADD . .

RUN mv docker-entrypoint.sh /usr/local/bin \
    && mkdir config \
    && mkdir cache \
    && chown www-data:www-data /var/www/html/config \
    && chown www-data:www-data /var/www/html/cache

EXPOSE 9000

USER www-data

# Persistent config file
VOLUME [ "/var/www/html/config", "/var/www/html/cache" ]

ENTRYPOINT [ "docker-entrypoint.sh" ]
CMD [ "php-fpm" ]
