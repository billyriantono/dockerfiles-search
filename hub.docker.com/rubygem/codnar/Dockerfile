FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.77

RUN gem install codnar --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["codnar-split"]
CMD ["--help"]
