FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.2

RUN gem install fredapi --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fredapi"]
CMD ["--help"]
