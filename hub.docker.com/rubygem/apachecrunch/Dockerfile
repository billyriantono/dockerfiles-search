FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6

RUN gem install apachecrunch --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["apachecrunch"]
CMD ["--help"]
