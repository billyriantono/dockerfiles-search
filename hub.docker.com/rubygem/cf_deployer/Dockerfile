FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.6.0

RUN gem install cf_deployer --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cf_deploy"]
CMD ["--help"]
