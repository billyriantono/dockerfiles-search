FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.0

RUN gem install heartbeat-client --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hbc"]
CMD ["--help"]
