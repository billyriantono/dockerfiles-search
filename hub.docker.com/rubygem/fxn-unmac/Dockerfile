FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.7

RUN gem install fxn-unmac --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["unmac"]
CMD ["--help"]
