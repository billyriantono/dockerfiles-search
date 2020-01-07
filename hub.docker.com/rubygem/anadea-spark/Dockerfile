FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.0

RUN gem install anadea-spark --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["spark"]
CMD ["--help"]
