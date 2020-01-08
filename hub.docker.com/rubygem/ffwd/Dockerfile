FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.7

RUN gem install ffwd --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ffwd"]
CMD ["--help"]
