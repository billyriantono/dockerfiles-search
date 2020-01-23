FROM ruby:2.6-alpine

RUN apk --update add musl-dev gcc make g++

RUN gem install cf-uaac -v 4.1.0 --no-document

ENTRYPOINT ["uaac"]