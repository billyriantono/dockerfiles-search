FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.25

RUN gem install deepsecurity --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dsc"]
CMD ["--help"]
