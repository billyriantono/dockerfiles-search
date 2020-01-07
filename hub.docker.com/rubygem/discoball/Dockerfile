FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.3

RUN gem install discoball --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["discoball"]
CMD ["--help"]
