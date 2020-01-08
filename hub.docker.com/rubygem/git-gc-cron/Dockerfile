FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install git-gc-cron --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-gc-cron"]
CMD ["--help"]
