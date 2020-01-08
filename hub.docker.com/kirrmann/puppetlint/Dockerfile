FROM alpine:latest
MAINTAINER Stefan Kirrmann <stefan.kirrmann@gmail.com>
RUN apk update && apk add \
  ruby \
  ruby-dev \
  ruby-irb \
  ruby-rdoc \
  && rm /var/cache/apk/* \
  && gem install puppet-lint
