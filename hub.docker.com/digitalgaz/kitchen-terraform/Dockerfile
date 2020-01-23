FROM hashicorp/terraform:latest

MAINTAINER digitalGaz <digitalgaz@hotmail.com>

ENV BUILD_PACKAGES bash curl-dev ruby-dev build-base

ENV RUBY_PACKAGES ruby ruby-io-console ruby-bundler

WORKDIR /tmp

ADD Gemfile .

RUN apk update && \
    apk upgrade && \
    apk add $BUILD_PACKAGES && \
    apk add $RUBY_PACKAGES && \
    bundle install && \
    rm -rf /var/cache/apk/* /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENTRYPOINT ["/bin/bash"]