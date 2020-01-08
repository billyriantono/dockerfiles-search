FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.6

RUN gem install imap_processor --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["imap_archive"]
CMD ["--help"]
