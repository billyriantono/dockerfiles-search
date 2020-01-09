FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.3

RUN gem install cgminer_api_client --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cgminer_api_client"]
CMD ["--help"]
