FROM ruby:2.6.3-alpine3.10

ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8

RUN apk add --update --no-cache build-base ruby-dev nodejs nodejs-npm yarn git && \
  gem install bundler --version 2.0.2
