FROM ruby:2.4.3-alpine

ENV LANG C.UTF-8
ENV LANGUAGE C.UTF-8
ENV LC_ALL C.UTF-8

# https://github.com/bundler/bundler/issues/6154
ENV BUNDLE_GEMFILE='./Gemfile'

RUN apk --no-cache add build-base libcurl

COPY . /app
WORKDIR /app

RUN bundle install && rm -rf /app
