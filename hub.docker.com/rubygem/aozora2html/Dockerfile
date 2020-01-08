FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.7.0

RUN gem install aozora2html --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["aozora2html"]
CMD ["--help"]
