FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.0

RUN gem install airhorn --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["airhorn"]
CMD ["--help"]
