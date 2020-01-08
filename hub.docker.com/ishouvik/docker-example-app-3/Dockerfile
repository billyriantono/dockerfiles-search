FROM ruby:2.3.1

RUN apt-get update && apt-get install -y build-essential nodejs mysql-client vim

RUN mkdir /app

WORKDIR /app

RUN gem install bundler

ADD Gemfile /app/Gemfile
ADD Gemfile.lock /app/Gemfile.lock

RUN bundle install
ADD . /app
