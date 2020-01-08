FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.3

RUN gem install imdb_parser --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["imdb"]
CMD ["--help"]
