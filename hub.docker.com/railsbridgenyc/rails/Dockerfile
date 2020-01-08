FROM ruby:2.5.3-slim

COPY dockerfile-version /etc/dockerfile-version

RUN apt-get update -qq && \
    apt-get install -y build-essential libpq-dev git vim nodejs postgresql-client build-essential && \
    gem install rails -v 5.2.1 && \
    cd /tmp && rails new some_app --database=postgresql

WORKDIR /workdir
