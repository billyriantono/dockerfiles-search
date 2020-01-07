FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.5

RUN gem install cf_factory --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cf_factory"]
CMD ["--help"]
