FROM ruby:2.1
MAINTAINER Federico Ramallo <framallo@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y -qq libicu-dev libkrb5-dev cmake nodejs qt5-default libqt5webkit5-dev xvfb
RUN rm -rf /var/lib/apt/lists/*
