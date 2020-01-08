FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.6

RUN gem install gemrat --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gemrat"]
CMD ["--help"]
