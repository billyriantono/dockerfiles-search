FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.0

RUN gem install couchup --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["couchup"]
CMD ["--help"]
