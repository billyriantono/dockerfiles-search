FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.21.0

RUN gem install haml_lint --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["haml-lint"]
CMD ["--help"]
