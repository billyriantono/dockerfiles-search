FROM ruby:2.3.0-alpine

MAINTAINER Cedric DIRAND <cedric.dirand@gmail.com>

ENV RAILS_VERSION 2.4.6

RUN apk --update add --no-cache \
    libxml2-dev \
    libxslt-dev \
    sqlite-dev \
    nodejs \
    tzdata \
    build-base

# Bug with libxml / libxst include in nokogiri, Necessary to
# compile before
RUN gem install nokogiri -- --use-system-libraries --with-xml2-include=/usr/include/libxml2 --with-xml2-lib=/usr/lib/

RUN gem install rails
