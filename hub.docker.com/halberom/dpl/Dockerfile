FROM ruby:2.3-alpine
MAINTAINER Gerard Lynch <gerard@halberom.co.uk>

RUN apk add --no-cache \
  curl \
  git

RUN gem install bundler --no-ri --no-rdoc && \
    gem install dpl --no-ri --no-rdoc

RUN mkdir /src
WORKDIR /src

CMD ["dpl"]
