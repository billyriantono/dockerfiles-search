FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.6

RUN gem install aws_pipes --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["aws_db"]
CMD ["--help"]
