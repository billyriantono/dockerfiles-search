FROM ruby:2.3

RUN mkdir /sa_users_app
RUN apt-get update
RUN apt-get install -y libc-ares2 libv8-3.14.5 nodejs
WORKDIR /sa_users_app

ADD Gemfile /sa_users_app/Gemfile
ADD Gemfile.lock /sa_users_app/Gemfile.lock

RUN bundle install
ADD . /sa_users_app

EXPOSE 3007
