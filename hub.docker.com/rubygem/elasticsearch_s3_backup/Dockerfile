FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0.3

RUN gem install elasticsearch_s3_backup --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["es_s3_backup"]
CMD ["--help"]
