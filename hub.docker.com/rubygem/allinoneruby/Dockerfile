FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.9

RUN gem install allinoneruby --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["allinoneruby"]
CMD ["--help"]
