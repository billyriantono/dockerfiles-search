FROM alpine:3.7

ENV RUBY_VERSION 2.5.0

RUN apk --update add --virtual .build-deps \
    bash \
    build-base \
    curl \
    g++ \
    gcc \
    git \
    gnupg \
    libressl-dev \
    libxml2-dev \
    libxslt-dev \
    linux-headers \
    readline-dev \
    tar \
    xz && \
  git clone http://github.com/rbenv/ruby-build.git /root/ruby-build && \
  /root/ruby-build/install.sh && \
  rm -rf /root/ruby-build && \
  ruby-build $RUBY_VERSION /usr/local && \
  gem install bundler && \
  apk del .build-deps && \
  mkdir -p /usr/src/app

WORKDIR /usr/src/app
