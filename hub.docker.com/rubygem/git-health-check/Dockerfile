FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install git-health-check --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ghc"]
CMD ["--help"]
