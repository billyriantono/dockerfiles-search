FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.8

RUN gem install cyclop --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cyclop"]
CMD ["--help"]
