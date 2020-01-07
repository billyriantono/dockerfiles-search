FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.3

RUN gem install cepmon-nagios --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["check_cepmon"]
CMD ["--help"]
