FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3

RUN gem install imdb_celebrity --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["imdb_celebrity"]
CMD ["--help"]
