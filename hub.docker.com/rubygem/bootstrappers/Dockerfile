FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=4.2.1.1

RUN gem install bootstrappers --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["bootstrappers"]
CMD ["--help"]
