FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=5.4.7

RUN gem install cf --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cf"]
CMD ["--help"]
