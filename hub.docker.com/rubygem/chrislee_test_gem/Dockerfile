FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.5

RUN gem install chrislee_test_gem --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["test_gem"]
CMD ["--help"]
