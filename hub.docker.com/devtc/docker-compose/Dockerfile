ARG DOCKER_VERSION=stable
FROM docker:${DOCKER_VERSION}

ARG DOCKER_VERSION

RUN apk add --no-cache --virtual .app-deps\
        bash \
        git \
        py-pip \
        gettext \
        python-dev \
        libffi-dev \
        openssl-dev \
        gcc \
        libc-dev \
        make gettext\
    && pip install docker-compose
