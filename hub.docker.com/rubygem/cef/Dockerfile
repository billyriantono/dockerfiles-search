FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.1.1.pre

RUN gem install cef --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cef_sender"]
CMD ["--help"]
