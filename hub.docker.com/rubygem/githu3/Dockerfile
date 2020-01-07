FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.8

RUN gem install githu3 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["githu3"]
CMD ["--help"]
