FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install aws_tracker --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["tracker"]
CMD ["--help"]
