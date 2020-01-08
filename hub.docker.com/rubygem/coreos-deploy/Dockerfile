FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.0

RUN gem install coreos-deploy --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["coreos"]
CMD ["--help"]
