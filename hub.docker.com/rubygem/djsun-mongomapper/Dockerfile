FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.1.2

RUN gem install djsun-mongomapper --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["mmconsole"]
CMD ["--help"]
