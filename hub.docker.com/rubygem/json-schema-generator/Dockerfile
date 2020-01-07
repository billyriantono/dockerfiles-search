FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install json-schema-generator --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["json-schema-generator"]
CMD ["--help"]
