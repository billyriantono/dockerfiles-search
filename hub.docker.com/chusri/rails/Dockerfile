FROM ruby:2.4.2-alpine
MAINTAINER Bank

RUN apk update
RUN apk upgrade

RUN apk add curl wget bash git libpq nodejs tzdata libxslt

RUN gem install bundler --no-document

RUN apk --update add --virtual build_deps \
    build-base libc-dev linux-headers \
    openssl-dev postgresql-dev libxml2-dev libxslt-dev && \
    bundle config build.nokogiri --use-system-libraries

RUN mkdir /usr/app
WORKDIR /usr/app

# ADD . /usr/app
# RUN bin/bundle install
