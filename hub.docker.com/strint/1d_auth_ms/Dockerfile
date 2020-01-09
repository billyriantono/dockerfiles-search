FROM ruby:2.3

RUN mkdir /1d_auth_ms
WORKDIR /1d_auth_ms

ADD Gemfile /1d_auth_ms/Gemfile
ADD Gemfile.lock /1d_auth_ms/Gemfile.lock


RUN bundle install

ADD . /1d_auth_ms

EXPOSE 8001
