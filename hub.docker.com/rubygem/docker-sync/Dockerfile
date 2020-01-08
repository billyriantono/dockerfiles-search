FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.0

RUN gem install docker-sync --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["docker-sync"]
CMD ["--help"]
