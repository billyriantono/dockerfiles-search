FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.0

RUN gem install git_multicast --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git_multicast"]
CMD ["--help"]
