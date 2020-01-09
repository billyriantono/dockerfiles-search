FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.99.0

RUN gem install corto --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["corto"]
CMD ["--help"]
