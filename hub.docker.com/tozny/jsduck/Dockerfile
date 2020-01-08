# Dockerfile written by Eric Mann <eric@tozny.com>
#
# Work derived from docker-jsduck by Sergei Lissovski <http://github.com/sergeil>:
#
# Copyright (c) 2016 Tozny, LLC

FROM alpine:3.4

MAINTAINER Eric Mann <eric@tozny.com>

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

ENV JSDUCK_VERSION 5.3.4

RUN set -x \
    && apk add --no-cache --virtual .build-deps \
        alpine-sdk \
    && apk add --no-cache \
        ruby \
        ruby-dev \
    && gem install --no-ri --no-rdoc jsduck -v $JSDUCK_VERSION \
    && apk del .build-deps \
    && rm -rf ~/.cache /var/cache/apk/* /tmp/*

RUN mkdir workdir && cd workdir

WORKDIR /workdir

CMD ["/bin/sh"]