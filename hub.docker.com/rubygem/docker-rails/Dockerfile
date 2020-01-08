FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.0

RUN gem install docker-rails --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["docker-rails"]
CMD ["--help"]
