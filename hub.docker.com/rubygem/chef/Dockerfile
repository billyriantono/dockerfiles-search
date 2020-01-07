FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=12.9.41

RUN gem install chef --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["chef-client"]
CMD ["--help"]
