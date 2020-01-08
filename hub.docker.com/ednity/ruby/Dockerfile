FROM ruby:2.3.1

RUN apt-get update -qq

WORKDIR /

ADD Gemfile /Gemfile
ADD Gemfile.lock /Gemfile.lock

RUN bundle install
