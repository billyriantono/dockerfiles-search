FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.1.9

RUN gem install haml-edge --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["haml"]
CMD ["--help"]
