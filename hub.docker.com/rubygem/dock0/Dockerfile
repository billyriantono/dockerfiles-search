FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.2

RUN gem install dock0 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dock0"]
CMD ["--help"]
