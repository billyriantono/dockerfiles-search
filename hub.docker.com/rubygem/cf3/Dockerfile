FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.5

RUN gem install cf3 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cf3samples"]
CMD ["--help"]
