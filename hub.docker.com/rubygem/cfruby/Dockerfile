FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.01

RUN gem install cfruby --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cfenjin"]
CMD ["--help"]
