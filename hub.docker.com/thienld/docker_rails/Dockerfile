# Based on https://docs.docker.com/compose/rails/

# Following image already has bundler installed.
FROM ruby:2.2

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

RUN mkdir /myapp

WORKDIR /myapp

ADD Gemfile /myapp/Gemfile

ADD Gemfile.lock /myapp/Gemfile.lock

RUN bundle install

ADD . /myapp
