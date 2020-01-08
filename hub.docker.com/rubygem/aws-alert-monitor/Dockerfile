FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.0

RUN gem install aws-alert-monitor --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["aws-alert-monitor"]
CMD ["--help"]
