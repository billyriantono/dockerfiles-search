FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.3

RUN gem install gembox --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gembox"]
CMD ["--help"]
