FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.2

RUN gem install hostmanager --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hm"]
CMD ["--help"]
