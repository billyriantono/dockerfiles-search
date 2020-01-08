FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.5

RUN gem install gitty --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-hook"]
CMD ["--help"]
