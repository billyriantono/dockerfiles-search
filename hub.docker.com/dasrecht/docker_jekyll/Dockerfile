from ruby:latest

RUN apt-get update && \
    apt-get install -y rsync imagemagick jpegoptim && \
    rm -rf /var/lib/apt/lists/*

ADD Gemfile .
ADD Gemfile.lock .

RUN bundle install
