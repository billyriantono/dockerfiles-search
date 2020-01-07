FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.41.0

RUN gem install gen --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gen"]
CMD ["--help"]
