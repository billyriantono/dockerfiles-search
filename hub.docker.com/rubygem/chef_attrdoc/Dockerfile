FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.0

RUN gem install chef_attrdoc --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["chef_attrdoc"]
CMD ["--help"]
