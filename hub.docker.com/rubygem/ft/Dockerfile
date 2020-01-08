FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3

RUN gem install ft --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ft"]
CMD ["--help"]
