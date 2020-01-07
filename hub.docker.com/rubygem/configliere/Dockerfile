FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.8

RUN gem install configliere --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["configliere"]
CMD ["--help"]
