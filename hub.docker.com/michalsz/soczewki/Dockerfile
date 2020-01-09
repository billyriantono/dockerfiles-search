FROM ruby:2.5.3-alpine
RUN apk update && apk add --update curl-dev ruby-dev build-base bash
RUN apk add postgresql-dev sqlite-dev
RUN apk add ruby-json yaml nodejs

RUN mkdir /app
WORKDIR /app
ADD Gemfile /app/Gemfile
#ADD Gemfile.lock /app/Gemfile.lock
RUN bundle install
ADD . /app
