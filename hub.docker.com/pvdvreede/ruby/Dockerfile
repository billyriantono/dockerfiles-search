FROM debian:latest
MAINTAINER Paul Van de Vreede <paul@vdvreede.net>

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
ENV RUBY_VERSION 2.1.4
RUN curl https://s3.amazonaws.com/pkgr-buildpack-ruby/current/debian-7/ruby-$RUBY_VERSION.tgz -o - | tar xzf - -C /usr/local

