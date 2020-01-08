FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install appium_doc_lint --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["appium_doc_lint"]
CMD ["--help"]
