FROM bakerdist/magento2-php:2.3-php7.2-cli-buster

RUN apt-get update && apt-get install -y \
        git \
        patch \
        tini \
    && rm -rf /var/lib/apt/lists/*

COPY --from=composer:1.9 /usr/bin/composer /usr/bin/composer

COPY docker-composer-* /usr/local/bin

ENTRYPOINT ["docker-composer-entrypoint"]

CMD ["composer"]

USER magento

RUN composer global require hirak/prestissimo
