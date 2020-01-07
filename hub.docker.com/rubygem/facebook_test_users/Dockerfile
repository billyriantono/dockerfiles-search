FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.4

RUN gem install facebook_test_users --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fbtu"]
CMD ["--help"]
