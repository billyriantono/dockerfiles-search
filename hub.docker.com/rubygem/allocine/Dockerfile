FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.2

RUN gem install allocine --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["allocine-web"]
CMD ["--help"]
