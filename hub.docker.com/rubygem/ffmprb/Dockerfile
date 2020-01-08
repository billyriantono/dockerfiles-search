FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.6

RUN gem install ffmprb --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ffmprb"]
CMD ["--help"]
