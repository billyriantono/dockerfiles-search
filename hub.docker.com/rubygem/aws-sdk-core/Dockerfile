FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.0.0.rc3

RUN gem install aws-sdk-core --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["aws.rb"]
CMD ["--help"]
