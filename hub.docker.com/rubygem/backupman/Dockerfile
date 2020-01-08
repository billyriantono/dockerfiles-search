FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.5

RUN gem install BackupMan --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["backup_man"]
CMD ["--help"]
