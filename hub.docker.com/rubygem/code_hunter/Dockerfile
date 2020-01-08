FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.7

RUN gem install code_hunter --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["code_hunter"]
CMD ["--help"]
