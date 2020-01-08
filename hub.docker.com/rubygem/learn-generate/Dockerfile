FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.16

RUN gem install learn-generate --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["learn-generate"]
CMD ["--help"]
