FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.8

RUN gem install deckard --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["deckard"]
CMD ["--help"]
