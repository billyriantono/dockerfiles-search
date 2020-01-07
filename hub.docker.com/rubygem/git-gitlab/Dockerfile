FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.7

RUN gem install git-gitlab --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-gitlab"]
CMD ["--help"]
