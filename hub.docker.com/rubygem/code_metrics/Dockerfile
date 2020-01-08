FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.3

RUN gem install code_metrics --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["code_metrics"]
CMD ["--help"]
