FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.1.1

RUN gem install cloudapp --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cloudapp"]
CMD ["--help"]
