FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.0.pre

RUN gem install 7_half --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["7_half"]
CMD ["--help"]
