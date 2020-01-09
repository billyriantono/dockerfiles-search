#
# Composer Dockerfile
# version 1.0
#
FROM youpin/php
MAINTAINER Leo <jiangwenhua@yoyohr.com>

WORKDIR /tmp

RUN \
    apt-get update \
    && DEBIAN_FRONTEND="noninteractive" apt-get install -y git \
    && curl -sS https://install.phpcomposer.com/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update \
    && apt-get remove --purge curl -y \
    && apt-get clean

VOLUME /home/data

ENTRYPOINT ["composer"]
CMD ["--help"]
