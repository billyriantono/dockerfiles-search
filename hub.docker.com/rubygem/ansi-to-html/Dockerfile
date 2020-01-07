FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3

RUN gem install ansi-to-html --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ansi-to-html"]
CMD ["--help"]
