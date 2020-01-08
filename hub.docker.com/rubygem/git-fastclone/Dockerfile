FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.2

RUN gem install git-fastclone --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-fastclone"]
CMD ["--help"]
