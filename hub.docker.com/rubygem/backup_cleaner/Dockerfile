FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.1

RUN gem install backup_cleaner --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["backup_cleaner"]
CMD ["--help"]
