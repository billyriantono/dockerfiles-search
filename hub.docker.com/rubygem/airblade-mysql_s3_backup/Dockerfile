FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install airblade-mysql_s3_backup --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["mysql_s3_backup"]
CMD ["--help"]
