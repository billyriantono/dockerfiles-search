FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3

RUN gem install habiter --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["habiter"]
CMD ["--help"]
