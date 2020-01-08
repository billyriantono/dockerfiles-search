FROM ruby:2.4-stretch

ENV TERM=xterm PATH=/app/bin:$PATH DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
 && apt-get install -y xmlsec1 libgit2-dev cmake \
 && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
 && apt-get install -y nodejs \
 && apt-get install libmariadbclient-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && mkdir -p /app

WORKDIR /app
