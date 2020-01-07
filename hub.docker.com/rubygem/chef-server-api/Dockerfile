FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=10.30.4

RUN gem install chef-server-api --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["chef-server"]
CMD ["--help"]
