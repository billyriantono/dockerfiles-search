FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.20

RUN gem install iplayer-dl --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["iplayer-dl"]
CMD ["--help"]
