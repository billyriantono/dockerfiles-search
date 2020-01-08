FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.0

RUN gem install apdex --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["apdex_from_log"]
CMD ["--help"]
