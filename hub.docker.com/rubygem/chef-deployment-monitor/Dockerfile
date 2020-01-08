FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.3

RUN gem install chef-deployment-monitor --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["chef-logmon"]
CMD ["--help"]
