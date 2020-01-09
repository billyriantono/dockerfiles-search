FROM herloct/phpcs:3.3.2 as phpcs
FROM php:7.2.15-cli-alpine

ENV PHPCOMPATIBILITY_VERSION=9.1.1

COPY --from=phpcs /usr/local/bin/phpcs /usr/local/bin/phpcs

RUN echo 'memory_limit = -1' >> /usr/local/etc/php/conf.d/docker-php-memlimit.ini;

RUN curl -s -L https://github.com/PHPCompatibility/PHPCompatibility/archive/$PHPCOMPATIBILITY_VERSION.zip > /tmp/comp.zip \
    && unzip -q /tmp/comp.zip -d /usr/local \
    && rm /tmp/comp.zip \
    && phpcs --config-set installed_paths /usr/local/PHPCompatibility-$PHPCOMPATIBILITY_VERSION \
    && phpcs --config-set default_standard PHPCompatibility \
    && phpcs --config-set colors 1

WORKDIR /src
CMD "phpcs"