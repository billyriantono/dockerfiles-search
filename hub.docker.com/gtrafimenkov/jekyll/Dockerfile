FROM ubuntu:16.04

MAINTAINER gennady.trafimenkov@gmail.com

RUN apt-get update \
  && apt-get install -y ruby ruby-dev build-essential \
  && gem install jekyll bundler

ENTRYPOINT ["/usr/local/bin/jekyll"]
