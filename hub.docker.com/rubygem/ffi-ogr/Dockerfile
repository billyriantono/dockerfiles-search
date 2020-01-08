FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.0.pre

RUN gem install ffi-ogr --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ogr_console"]
CMD ["--help"]
