FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.8

RUN gem install docfu --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["docfu"]
CMD ["--help"]
