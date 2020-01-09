FROM ruby:2.5-alpine

RUN apk update && apk add --no-cache coreutils git make g++ nodejs && \
    git clone https://github.com/lord/slate /app && \
    cd /app && bundle install
WORKDIR /app