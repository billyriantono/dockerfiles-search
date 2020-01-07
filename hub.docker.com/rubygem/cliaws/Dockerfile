FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.7.7

RUN gem install cliaws --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["clis3"]
CMD ["--help"]
