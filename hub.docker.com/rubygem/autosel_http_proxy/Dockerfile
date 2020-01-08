FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.5

RUN gem install autosel_http_proxy --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["set_httpproxy"]
CMD ["--help"]
