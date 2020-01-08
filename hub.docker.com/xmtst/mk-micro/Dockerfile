FROM ruby:2.6.5-alpine

ENV LANG C.UTF-8
ENV TZ=Asia/Tokyo
ENV RAILS_ROOT=/srv/app/current

RUN mkdir -p $RAILS_ROOT

WORKDIR $RAILS_ROOT

ADD ./Gemfile $RAILS_ROOT/Gemfile
ADD ./Gemfile.lock $RAILS_ROOT/Gemfile.lock

RUN apk update && apk upgrade
RUN apk add --update --no-cache --virtual=.build-dependencies \
      curl-dev \
      linux-headers \
      libxml2-dev \
      libxslt-dev \
      ruby-dev \
      yaml-dev \
      zlib-dev \
      mysql-dev \
      build-base && \
    apk add --update --no-cache \
      bash \
      openssh \
      openssl \
      ruby-json \
      mysql-client \
      mariadb-dev \
      tzdata \
      yaml && \
    gem install bundler:2.0.1 && \
    bundle install -j4 && \
    apk del .build-dependencies

ENV DOCKERIZE_VERSION=v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz
RUN tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz
RUN rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz
