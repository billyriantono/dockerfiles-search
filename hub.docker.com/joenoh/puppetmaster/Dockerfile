FROM ubuntu:16.04
MAINTAINER Joe Honzawa <honzawa.j@pepabo.com>

RUN apt-get update \
  && apt-get install -yqq --no-install-recommends puppetmaster=3.8.5-2 ruby=1:2.3.0+1 \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
RUN gem install bundler --no-document

RUN service puppetmaster start
