FROM ruby:2.5-alpine

RUN apk add --no-cache build-base gcc bash cmake perl
RUN apk add --no-cache bc curl

COPY cowsay /usr/local/bin/cowsay
COPY docker.cow /usr/local/share/cows/default.cow

RUN gem install jekyll

EXPOSE 4000

RUN mkdir -p /usr/app/
ADD ./ /usr/app/
WORKDIR /usr/app/
