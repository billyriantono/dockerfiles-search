FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3

RUN gem install haml-server --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["haml-server"]
CMD ["--help"]
