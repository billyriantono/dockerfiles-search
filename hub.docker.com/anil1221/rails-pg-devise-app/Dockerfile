FROM ruby:2.5.1

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

RUN mkdir /postgres-docker
WORKDIR /postgres-docker

ADD Gemfile /postgres-docker/Gemfile
ADD Gemfile.lock /postgres-docker/Gemfile.lock

RUN bundle install

ADD . /postgres-docker