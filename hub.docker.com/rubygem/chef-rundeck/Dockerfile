FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.2.0

RUN gem install chef-rundeck --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["chef-rundeck"]
CMD ["--help"]
