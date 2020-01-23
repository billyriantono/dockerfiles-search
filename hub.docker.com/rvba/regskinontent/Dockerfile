FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.8.3

RUN gem install httpclient --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["httpclient"]
CMD ["--help"]
