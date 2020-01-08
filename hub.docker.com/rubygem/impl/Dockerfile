FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2

RUN gem install impl --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["impl"]
CMD ["--help"]
