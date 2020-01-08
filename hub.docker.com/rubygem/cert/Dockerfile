FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0.0

RUN gem install cert --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cert"]
CMD ["--help"]
