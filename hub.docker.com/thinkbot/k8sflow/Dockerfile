FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.13.0

RUN gem install k8sflow --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["k8sflow"]
CMD ["--help"]
