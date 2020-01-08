FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install backup_jenkins --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["backup_jenkins"]
CMD ["--help"]
