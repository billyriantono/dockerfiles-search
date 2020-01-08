FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.4.0

RUN gem install learn-test --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["learn-test"]
CMD ["--help"]
