FROM ruby:2.6.3-alpine

RUN set -ex \
 && apk add --update --upgrade --no-cache \
    build-base \
    git \
    zlib-dev \
    libxml2 \
    libxml2-dev \
    libxslt \
    libxslt-dev \
    tzdata \
    yaml-dev \
    mysql-dev \
    mysql-client \
    nodejs=10.16.0-r0 \
    yaml

# Pre-install gems and configure bundle
RUN set -ex \
 && gem install -N nokogiri \
 && echo 'gem: --no-document --no-rdoc --no-ri' >> ~/.gemrc \
 && bundle config --global build.nokogiri --use-system-libraries

# WORKING DIR
RUN set -ex \
 && mkdir /webapp
WORKDIR /webapp
