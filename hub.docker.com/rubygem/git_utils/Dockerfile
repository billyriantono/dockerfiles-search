FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0.0

RUN gem install git_utils --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gem_publish"]
CMD ["--help"]
