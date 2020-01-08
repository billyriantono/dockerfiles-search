FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.3

RUN gem install concourse-github-status --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["check"]
CMD ["--help"]
