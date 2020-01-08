FROM ruby:2.5.1-slim
LABEL maintainer="cheimke@loumaris.com"

WORKDIR /app

EXPOSE 3000

RUN apt-get update && \
  apt-get install -y build-essential curl git nodejs imagemagick libpq-dev sqlite3 libsqlite3-dev && \
  gem install bundler

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
  && apt-get install -y nodejs





