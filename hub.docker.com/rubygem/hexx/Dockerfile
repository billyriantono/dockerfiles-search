FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=9.2.0

RUN gem install hexx --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hexx"]
CMD ["--help"]
