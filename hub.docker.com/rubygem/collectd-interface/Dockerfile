FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.1

RUN gem install collectd-interface --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["collectd-interface-daemon"]
CMD ["--help"]
