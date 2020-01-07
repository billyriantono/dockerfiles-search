FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0

RUN gem install gem_updater --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gem_update"]
CMD ["--help"]
