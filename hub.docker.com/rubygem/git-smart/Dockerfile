FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.9

RUN gem install git-smart --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-smart-log"]
CMD ["--help"]
