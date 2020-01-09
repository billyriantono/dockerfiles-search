FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.0.rc1

RUN gem install fluent-plugin-mongo --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["mongo-tail"]
CMD ["--help"]
