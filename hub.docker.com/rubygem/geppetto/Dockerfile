FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.8

RUN gem install geppetto --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["geppetto"]
CMD ["--help"]
