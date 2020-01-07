FROM ruby:2.4-slim
RUN apt-get update -qq && apt-get install -y \
  build-essential \
  curl \
  git \
  libpq-dev \
  npm
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
  apt-get install -y nodejs
#  nodejs \
#  nodejs-legacy \
WORKDIR /src
ADD Gemfile /src/Gemfile
ADD Gemfile.lock /src/Gemfile.lock
RUN bundle && gem install foreman
