FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.7

RUN gem install ffwd-tunnel --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ffwd-tunnel-agent"]
CMD ["--help"]
