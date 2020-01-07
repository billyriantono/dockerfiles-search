FROM ruby:alpine

RUN apk add --update build-base tzdata
RUN gem install jekyll bundler

WORKDIR /app
ADD Gemfile Gemfile.lock /app/
RUN bundle install
