FROM alpine:3.6

RUN echo "@edge http://nl.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories
RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

RUN apk --update --upgrade add --no-cache \
        bash \
        build-base \
        git \
        libc-dev \
        libffi \
        libffi-dev \
        libstdc++ \
        libxml2 \
        libxml2-dev \
        libxslt \
        libxslt-dev \
        libressl \
        libressl-dev \
        linux-headers \
        readline \
        readline-dev \
        ruby \
        ruby-bundler \
        ruby-dev \
        ruby-io-console \
        ruby-irb \
        ruby-json \
        ruby-rake \
        ruby-rdoc \
        ruby-bigdecimal \
        tzdata \
        yaml \
        yaml-dev \
        zlib \
        zlib-dev \
        ca-certificates && \
        rm /var/cache/apk/*

RUN echo 'gem: --no-document' > /etc/gemrc

RUN mkdir -p /app

WORKDIR /app

CMD ["irb"]
