FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.8

RUN gem install cloudfiles_cli --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cloudfiles_cli"]
CMD ["--help"]
