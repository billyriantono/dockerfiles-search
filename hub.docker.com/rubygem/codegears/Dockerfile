FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9.pre

RUN gem install codegears --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cg"]
CMD ["--help"]
