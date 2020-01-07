FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.7

RUN gem install aws-cfn-dsl --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cfn-dsl"]
CMD ["--help"]
