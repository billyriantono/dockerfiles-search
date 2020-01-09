FROM ruby:2.3

RUN mkdir /sa_api_ms
WORKDIR /sa_api_ms

ADD Gemfile /sa_api_ms/Gemfile
ADD Gemfile.lock /sa_api_ms/Gemfile.lock

RUN bundle install
ADD . /sa_api_ms

EXPOSE 4005
