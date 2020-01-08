FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3

RUN gem install clouddns --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["clouddns"]
CMD ["--help"]
