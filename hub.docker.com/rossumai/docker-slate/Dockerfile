FROM ruby:alpine

RUN apk add --no-cache nodejs
RUN apk add --no-cache --virtual .build-deps git coreutils make g++ && \
  git clone https://github.com/lord/slate /slate && \
  cd /slate && \
  bundle install && \
  apk del .build-deps
