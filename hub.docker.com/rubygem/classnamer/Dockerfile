FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.0.7

RUN gem install classnamer --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["classnamer"]
CMD ["--help"]
