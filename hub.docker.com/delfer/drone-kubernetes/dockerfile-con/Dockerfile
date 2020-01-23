FROM alpine:3.7

LABEL maintainer="David Guerrero <deivguerrero@gmail.com>"

ENV INSTALL_PATH /origin
RUN mkdir -p $INSTALL_PATH

WORKDIR $INSTALL_PATH

RUN apk add --no-cache --update --virtual .build-deps \
    ca-certificates \
    build-base \
    gcc \
    python3 \
    python3-dev \
    \
    && find /usr/local \
        \( -type d -a -name test -o -name tests \) \
        -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
        -exec rm -rf '{}' + \
    && runDeps="$( \
        scanelf --needed --nobanner --recursive /usr/local \
                | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
                | sort -u \
                | xargs -r apk info --installed \
                | sort -u \
    )" \
    && apk add --virtual .rundeps $runDeps \
    && apk del .build-deps