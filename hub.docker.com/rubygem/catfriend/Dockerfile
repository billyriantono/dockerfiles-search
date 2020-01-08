FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.20

RUN gem install catfriend --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["catfriend"]
CMD ["--help"]
