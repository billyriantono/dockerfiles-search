FROM ruby:2.5.1-alpine

RUN apk add bash curl

RUN apk add alpine-sdk -t build && \
  gem install engineyard -v '3.2.5' && \
  apk del build

RUN adduser -D circleci

USER circleci

ENTRYPOINT [ "/bin/bash" ]
