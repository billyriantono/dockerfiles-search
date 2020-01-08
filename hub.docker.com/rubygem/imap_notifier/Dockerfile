FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.9

RUN gem install imap_notifier --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["imap_notifier"]
CMD ["--help"]
