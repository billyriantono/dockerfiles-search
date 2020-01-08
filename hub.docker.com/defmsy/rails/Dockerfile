FROM ruby:2.3

RUN apt-get update && apt-get install -y nodejs --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN gem install rails --version 4.2.6

RUN mkdir -p /app

WORKDIR /app

CMD bundle install && rails s -p 3000 -b '0.0.0.0'