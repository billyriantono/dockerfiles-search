FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.2

RUN gem install ang_first_gem --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ang_first_gem"]
CMD ["--help"]
