FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.66.0

RUN gem install aws-sdk-v1 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["aws-rb"]
CMD ["--help"]
