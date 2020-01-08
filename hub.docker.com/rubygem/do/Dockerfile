FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.0.i

RUN gem install do --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["doit"]
CMD ["--help"]
