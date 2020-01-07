FROM ruby:2.2.5-alpine

LABEL com.tomasbasham.maintainer "Tomas Basham <me@tomasbasham.co.uk>" \
      com.tomasbasham.description "Ruby"

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ONBUILD COPY Gemfile /usr/src/app
ONBUILD COPY Gemfile.lock /usr/src/app

ONBUILD RUN bundle install
