FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3

RUN gem install gitan --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gitan"]
CMD ["--help"]
