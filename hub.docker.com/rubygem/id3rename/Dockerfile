FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.4

RUN gem install id3rename --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["id3rename"]
CMD ["--help"]
