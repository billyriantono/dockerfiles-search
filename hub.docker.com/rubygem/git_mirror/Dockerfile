FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5

RUN gem install git_mirror --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-mirror"]
CMD ["--help"]
