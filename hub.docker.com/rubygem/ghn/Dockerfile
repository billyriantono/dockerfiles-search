FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.4.1

RUN gem install ghn --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ghn"]
CMD ["--help"]
