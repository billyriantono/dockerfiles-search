ARG PHP_VERSION=7.3
ARG NODEJS_VERSION=12

FROM node:${NODEJS_VERSION}-slim as local_node
RUN ( \
        for f in node npm; do \
            [ -f /usr/local/bin/$f ] || exit; \
        done; \
    )

FROM php:${PHP_VERSION}-cli

LABEL PHP_IMAGE="${PHP_VERSION}-cli"
LABEL NODEJS_IMAGE="${NODEJS_VERSION}-slim"
LABEL PHP_DOCKER="https://hub.docker.com/_/php"
LABEL NODEJS_DOCKER="https://hub.docker.com/_/node"
LABEL COMPOSER_DOCKER="https://hub.docker.com/_/composer"
LABEL PROVIDES_BINS="php composer node npm"

COPY --from=composer /usr/bin/composer /usr/local/bin/composer
COPY --from=local_node /usr/local/lib/ /usr/local/lib/
COPY --from=local_node /usr/local/bin/node /usr/local/bin/
RUN ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm

RUN apt-get update; \
    apt-get install -y --no-install-recommends \
        zlib1g-dev; \
    \
    docker-php-ext-install zip; \
    \
    rm -rf /var/lib/apt/lists/*;

RUN apt-get update; \
    apt-get install -y --no-install-recommends \
        git \
        zip \
        unzip \
        tar \
        rsync \
        openssh-client; \
    rm -rf /var/lib/apt/lists/*;

ENV PATH=/tmp/vendor/bin/:$PATH

RUN mkdir /app
WORKDIR /app

ENTRYPOINT []
CMD [ "/bin/bash" ]
