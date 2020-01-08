FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.7.2

RUN gem install content_server --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["content_server"]
CMD ["--help"]
