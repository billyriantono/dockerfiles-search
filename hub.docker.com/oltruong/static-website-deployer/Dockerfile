FROM ruby:2.6.3-alpine

LABEL maintainer oltruong<contact@oltruong.com>

RUN apk add --update bash build-base libffi-dev openssh rsync nodejs-npm
RUN gem install bundler
RUN npm install -g firebase-tools
