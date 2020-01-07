FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9

RUN gem install ghtorrent --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ght-data-retrieval"]
CMD ["--help"]
