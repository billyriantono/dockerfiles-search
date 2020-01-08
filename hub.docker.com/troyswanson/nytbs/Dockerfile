FROM ruby:2.6.3

RUN apt-get update -qq && apt-get install -y build-essential

RUN apt-get install -y libpq-dev libxml2-dev libxslt1-dev nodejs

ENV APP_HOME /usr/src/app
WORKDIR $APP_HOME

COPY Gemfile* ./
RUN bundle install

ADD . $APP_HOME