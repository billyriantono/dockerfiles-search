FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.6

RUN gem install eb_deployer --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["eb_deploy"]
CMD ["--help"]
