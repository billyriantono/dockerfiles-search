FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.1

RUN gem install babot --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["babot"]
CMD ["--help"]
