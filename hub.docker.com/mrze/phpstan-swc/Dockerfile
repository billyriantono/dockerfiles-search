FROM mrze/swc-docker:php7

ENV COMPOSER_HOME /composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV PATH /composer/vendor/bin:$PATH

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN echo "memory_limit=-1" > /usr/local/etc/php/conf.d/99_memory-limit.ini \
    && composer global require phpstan/phpstan \
    && composer global require phpstan/phpstan-phpunit

VOLUME ["/app"]
WORKDIR /app
ENTRYPOINT []
