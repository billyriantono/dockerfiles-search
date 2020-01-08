FROM php:7.3-cli-alpine3.9

LABEL maintainer="frank.giesecke@final-gene.de"

ENV PHPCS_VERSION=3.4.2

RUN curl -LSs -o /usr/local/bin/phpcs "https://github.com/squizlabs/PHP_CodeSniffer/releases/download/${PHPCS_VERSION}/phpcs.phar" \
    && chmod a+x /usr/local/bin/phpcs

RUN curl -LSs -o /usr/local/bin/phpcbf "https://github.com/squizlabs/PHP_CodeSniffer/releases/download/${PHPCS_VERSION}/phpcbf.phar" \
    && chmod a+x /usr/local/bin/phpcbf

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

WORKDIR /app

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

CMD ["phpcs"]
