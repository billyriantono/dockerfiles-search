FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.8.3

RUN gem install kameleon-builder --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["kameleon"]
CMD ["--help"]
