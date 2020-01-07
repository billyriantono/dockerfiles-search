FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install git_test --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git_test"]
CMD ["--help"]
