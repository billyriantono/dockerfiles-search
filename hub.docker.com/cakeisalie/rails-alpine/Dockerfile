FROM ruby:2.5.1-alpine

RUN apk update && apk add tzdata build-base postgresql-dev nodejs yarn imagemagick

ENV TZ=Europe/Moscow

RUN mkdir /app
WORKDIR /app

