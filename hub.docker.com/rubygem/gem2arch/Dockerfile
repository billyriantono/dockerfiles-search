FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.7

RUN gem install gem2arch --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gem2arch"]
CMD ["--help"]
