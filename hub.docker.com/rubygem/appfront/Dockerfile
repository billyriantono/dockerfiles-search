FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.9

RUN gem install appfront --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["appfront"]
CMD ["--help"]
