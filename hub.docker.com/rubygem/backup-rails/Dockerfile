FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.5

RUN gem install backup-rails --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["backup_rails"]
CMD ["--help"]
