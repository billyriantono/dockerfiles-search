FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.6

RUN gem install chef-monitor --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["chef-logmon"]
CMD ["--help"]
