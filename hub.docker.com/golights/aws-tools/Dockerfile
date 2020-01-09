FROM alpine:latest

RUN apk --no-cache add \
        curl \
        less \
        groff \
        jq \
        python \
        py-pip \
        py2-pip

RUN pip install \
        awscli --upgrade

RUN apk update && \
    apk add \
        build-base \
        python-dev \
        libffi-dev \
        libxml2-dev \
        libxslt-dev \
        musl-dev \
        openssl-dev && \
    pip install aws-adfs && \
    apk del \
        python2-dev \
        openssl-dev \
        libssl1.0 \
        libcrypto1.0 \
        libgcrypt \
        libgpg-error \
        libxml2-dev \
        libxml2 \
        zlib-dev \
        libffi-dev \
        musl-utils \
        build-base \
        fortify-headers \
        make \
        g++ \
        libc-dev \
        musl-dev \
        gcc \
        mpc1 \
        mpfr3 \
        libatomic \
        libgomp \
        isl \
        gmp \
        binutils \
        binutils-libs && \
    rm -Rf /var/cache/apk/*

#        libxslt-dev \
#        libxslt \
