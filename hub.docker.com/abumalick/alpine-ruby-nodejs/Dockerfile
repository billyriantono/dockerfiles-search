FROM ruby:alpine
RUN apk --update add --virtual build-dependencies build-base ruby-dev openssl-dev libxml2-dev libxslt-dev \
    sqlite libc-dev linux-headers nodejs tzdata sqlite-dev && gem install bundler
