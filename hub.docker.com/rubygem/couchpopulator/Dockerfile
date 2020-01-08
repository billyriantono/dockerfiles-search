FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.0

RUN gem install couchpopulator --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["couchpopulator"]
CMD ["--help"]
