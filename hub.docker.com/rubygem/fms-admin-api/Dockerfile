FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3

RUN gem install fms-admin-api --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fmsapi"]
CMD ["--help"]
