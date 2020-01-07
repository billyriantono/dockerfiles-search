FROM php:7.3-cli-alpine3.10

COPY --from=composer /usr/bin/composer /usr/local/bin/composer

WORKDIR /var/steevanb/php-code-sniffs

RUN \
    echo '{"require": {"steevanb/php-code-sniffs": "3.0.*"}}' > composer.json \
    && composer update --no-dev --classmap-authoritative

ENV PHPCS_PARAMETERS=""
ENV PHPCS_BOOTSTRAP=""

COPY entrypoint.sh /var/entrypoint.sh
RUN chmod +x /var/entrypoint.sh

ENTRYPOINT ["/var/entrypoint.sh"]
