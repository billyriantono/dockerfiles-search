FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.0

RUN gem install git-p4-sync --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-p4-sync"]
CMD ["--help"]
