FROM ruby:latest

RUN mkdir -p /usr/src/Gemfile
WORKDIR /usr/src/Gemfile
RUN apt-get update && apt-get install -y mysql-client postgresql-client sqlite3 nodejs imagemagick --no-install-recommends && rm -rf /var/lib/apt/lists/*
ENV LANG en_US.UTF-8
RUN gem source -r https://rubygems.org/
RUN gem source -a https://gems.ruby-china.com
ONBUILD COPY Gemfile .
ONBUILD COPY Gemfile.lock .
ONBUILD RUN bundle install
