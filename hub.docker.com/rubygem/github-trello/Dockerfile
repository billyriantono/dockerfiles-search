FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.3

RUN gem install github-trello --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["trello-web"]
CMD ["--help"]
