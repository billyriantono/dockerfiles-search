FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9

RUN gem install aspelllint --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["aspelllint"]
CMD ["--help"]
