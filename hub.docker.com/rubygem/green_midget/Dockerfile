FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.2

RUN gem install green_midget --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["greenmidget"]
CMD ["--help"]
