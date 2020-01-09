FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=Izanami-0.13.0

RUN gem install izanami --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["izanami"]
CMD ["--help"]
