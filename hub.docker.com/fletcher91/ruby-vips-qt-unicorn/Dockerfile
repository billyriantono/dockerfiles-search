FROM ruby:2.6.5
MAINTAINER Thom van Kalkeren [fletcher91] <thom@argu.co>

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev libvips-dev libgsf-1-dev libxml2 zlib1g-dev qt5-default libqt5webkit5-dev unicorn
RUN apt-get install -y nodejs postgresql-client --no-install-recommends && rm -rf /var/lib/apt/lists/*

