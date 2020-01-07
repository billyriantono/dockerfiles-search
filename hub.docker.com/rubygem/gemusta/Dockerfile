FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.2

RUN gem install gemusta --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gemusta"]
CMD ["--help"]
