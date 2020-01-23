FROM ruby:2.5.0-alpine3.7
MAINTAINER Atsushi Nagase<a@ngs.io>

RUN gem install --no-rdoc --no-ri rubocop
ENTRYPOINT ["/usr/local/bundle/bin/rubocop"]
