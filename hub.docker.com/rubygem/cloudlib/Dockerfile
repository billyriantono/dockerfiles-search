FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.11

RUN gem install cloudlib --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cloudlib"]
CMD ["--help"]
