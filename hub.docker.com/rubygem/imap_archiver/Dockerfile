FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.8

RUN gem install imap_archiver --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["imap_archiver"]
CMD ["--help"]
