FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.2

RUN gem install dir_friend --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dir_friend"]
CMD ["--help"]
