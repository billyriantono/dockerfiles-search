FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.0

RUN gem install chatr --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["chatr_host"]
CMD ["--help"]
