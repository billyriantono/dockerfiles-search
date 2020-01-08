FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.9

RUN gem install appium_connect --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["AppiumConnect"]
CMD ["--help"]
