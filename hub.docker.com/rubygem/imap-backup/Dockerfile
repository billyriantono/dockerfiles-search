FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.0

RUN gem install imap-backup --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["imap-backup"]
CMD ["--help"]
