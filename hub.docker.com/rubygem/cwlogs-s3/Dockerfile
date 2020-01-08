FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.6

RUN gem install cwlogs-s3 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cwlogs-s3"]
CMD ["--help"]
