FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.8

RUN gem install git_remote_branch --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-remote-branch"]
CMD ["--help"]
