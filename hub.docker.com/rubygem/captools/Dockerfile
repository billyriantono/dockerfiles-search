FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3

RUN gem install captools --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["captools"]
CMD ["--help"]
