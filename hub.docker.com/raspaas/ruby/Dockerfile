FROM ruby:2.2.2

ENV PORT 5000
EXPOSE 5000

RUN mkdir /app
WORKDIR /app

ONBUILD ADD ./Gemfile Gemfile
ONBUILD ADD ./Gemfile.lock Gemfile.lock
ONBUILD RUN bundle install

ONBUILD ADD . /app
