FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.1

RUN gem install backup_aws_s3 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["backup_aws_s3"]
CMD ["--help"]
