FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.0

RUN gem install gem_version_check --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gem_version_check"]
CMD ["--help"]
