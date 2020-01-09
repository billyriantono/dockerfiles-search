FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=5.3.4

RUN gem install ansi2html --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ansi2html"]
CMD ["--help"]
