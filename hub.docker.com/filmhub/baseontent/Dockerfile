FROM ruby:2.3.1
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs
RUN mkdir /tevet_api
WORKDIR /tevet_api
ADD Gemfile /tevet_api/Gemfile
ADD Gemfile.lock /tevet_api/Gemfile.lock
RUN bundle install
ADD . /tevet_api
