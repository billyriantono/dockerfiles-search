FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.7.3

RUN gem install learn_linter --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["learn-lint"]
CMD ["--help"]
