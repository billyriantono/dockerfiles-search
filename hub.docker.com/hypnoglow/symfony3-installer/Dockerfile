FROM php:7.1-alpine
LABEL maintainer Igor Zibarev <zibarev.i@gmail.com>

RUN curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony \
    && chmod a+x /usr/local/bin/symfony

VOLUME /data

WORKDIR /data

ENTRYPOINT ["symfony"]
