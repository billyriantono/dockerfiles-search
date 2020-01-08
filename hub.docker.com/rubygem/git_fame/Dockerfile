FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.5.2

RUN gem install git_fame --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-fame"]
CMD ["--help"]
