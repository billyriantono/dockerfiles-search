FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.7

RUN gem install apache-config-generator --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["apache-configurator"]
CMD ["--help"]
