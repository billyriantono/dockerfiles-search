FROM ruby:2.3.1

RUN apt-get update -qq
RUN apt-get install -y nodejs

ARG APP_ROOT=/source
RUN mkdir $APP_ROOT
WORKDIR $APP_ROOT

COPY Gemfile* $APP_ROOT/
RUN bundle install

COPY . $APP_ROOT
