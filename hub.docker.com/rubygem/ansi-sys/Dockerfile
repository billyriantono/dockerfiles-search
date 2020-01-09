FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.8.3

RUN gem install ansi-sys --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ansi-to-html"]
CMD ["--help"]
