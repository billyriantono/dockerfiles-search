FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.0

RUN gem install git-pr-release --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-pr-release"]
CMD ["--help"]
