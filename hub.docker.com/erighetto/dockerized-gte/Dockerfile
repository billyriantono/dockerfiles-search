FROM ruby:2-slim

RUN apt-get update && apt-get dist-upgrade -y && apt install git -y

RUN gem install git_time_extractor

RUN apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir /usr/app

WORKDIR /usr/app