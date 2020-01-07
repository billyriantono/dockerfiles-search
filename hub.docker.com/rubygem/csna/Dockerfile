FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.003

RUN gem install csna --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["csna"]
CMD ["--help"]
