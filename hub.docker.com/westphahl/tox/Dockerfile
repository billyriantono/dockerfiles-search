FROM alpine:3.8

RUN apk add --no-cache \
        build-base \
        ca-certificates \
        libffi-dev \
        libjpeg \
        libjpeg-turbo-dev \
        libsass \
        postgresql-dev \
        openssh \
        libressl \
        libressl-dev \
        python3 \
        python3-dev \
        rsync \
        zlib-dev \
    && ln -s /usr/bin/python3 /usr/bin/python \
    && pip3 install --no-cache-dir tox
