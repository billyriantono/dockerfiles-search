FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.9

RUN gem install fOOrth --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fOOrth"]
CMD ["--help"]
