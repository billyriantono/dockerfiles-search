FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.0

RUN gem install hip --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hip"]
CMD ["--help"]
