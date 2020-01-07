FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.7

RUN gem install analyticator --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["analyticator"]
CMD ["--help"]
