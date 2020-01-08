FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.07

RUN gem install AmazonEchoJS --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["echo_monitor"]
CMD ["--help"]
