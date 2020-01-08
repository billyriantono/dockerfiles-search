FROM ruby:2.6.4-stretch

RUN apt-get -y update && apt-get -y install postgresql-client-common

RUN gem install bundler -v 1.17.3

ADD Gemfile* ./

RUN bundle
