FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.7

RUN gem install ganapati --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hdfs_thrift_server"]
CMD ["--help"]
