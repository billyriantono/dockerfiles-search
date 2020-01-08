FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.7.0

RUN gem install learn-co --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["learn"]
CMD ["--help"]
