FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.4.0

RUN gem install cf_light_api --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cf_light_api"]
CMD ["--help"]
