FROM ubuntu:16.04
MAINTAINER Krzysztof Suszyński <krzysztof.suszynski@coi.gov.pl>
RUN apt-get update \
  && apt-get install -y \
    ruby \
    ruby-dev \
    rubygems \
    build-essential \
    rpm \
  && rm -rf /var/lib/apt/lists/*
RUN gem install --no-ri --no-rdoc fpm
