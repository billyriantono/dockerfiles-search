FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.5

RUN gem install consul-template-generator --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["consul-template-generator"]
CMD ["--help"]
