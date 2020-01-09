FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.0

RUN gem install firebrew --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["firebrew"]
CMD ["--help"]
