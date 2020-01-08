FROM php:7.3-cli-alpine3.10

LABEL maintainer="frank.giesecke@final-gene.de"

ENV PHPMD_VERSION=2.7.0

WORKDIR /opt

# hadolint ignore=DL3018
RUN apk add --no-cache bash

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN curl -LSs "https://github.com/phpmd/phpmd/archive/${PHPMD_VERSION}.tar.gz" | tar -xz

WORKDIR /opt/phpmd-"${PHPMD_VERSION}"

RUN curl -LSs http://getcomposer.org/installer | php \
    && COMPOSER_ALLOW_SUPERUSER=1 php composer.phar install --no-dev --optimize-autoloader \
    && rm composer.phar \
    && ln -s "$(realpath src/bin/phpmd)" /usr/local/bin/phpmd

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

WORKDIR /app

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

CMD [""]
