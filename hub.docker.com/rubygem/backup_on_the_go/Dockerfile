FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.3

RUN gem install backup_on_the_go --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["backup-on-the-go"]
CMD ["--help"]
