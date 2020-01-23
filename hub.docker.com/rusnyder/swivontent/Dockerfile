FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.1

RUN gem install haml_parser --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["haml_parser"]
CMD ["--help"]
