FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1

RUN gem install imap_to_rss --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["imap_to_rss"]
CMD ["--help"]
