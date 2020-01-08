FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.3

RUN gem install learn-open --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["learn-open"]
CMD ["--help"]
