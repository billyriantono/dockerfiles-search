FROM ruby:2-alpine

RUN apk add --no-cache git
RUN apk add --no-cache alpine-sdk        && \
    gem install travis --no-rdoc --no-ri && \
    apk del --no-cache alpine-sdk


WORKDIR /work

LABEL name='travis'
LABEL version="1.0"

ENTRYPOINT ["travis"]
