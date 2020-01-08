FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.3

RUN gem install aws_configurer --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["aws_configurer"]
CMD ["--help"]
