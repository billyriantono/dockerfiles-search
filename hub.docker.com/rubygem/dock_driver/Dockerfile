FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.5

RUN gem install dock_driver --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dock_driver"]
CMD ["--help"]
