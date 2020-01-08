FROM node:10

MAINTAINER Andrii Krymets <applemintua@outlook.com>

RUN npm install -gq gulp && \
    yarn && \
    mkdir -p ${APP_BASE_DIR:-/var/www/}

WORKDIR ${APP_BASE_DIR:-/var/www/}
