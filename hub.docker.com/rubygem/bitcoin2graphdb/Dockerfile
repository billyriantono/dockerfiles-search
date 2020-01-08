FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.5

RUN gem install bitcoin2graphdb --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["bitcoin2graphdb"]
CMD ["--help"]
