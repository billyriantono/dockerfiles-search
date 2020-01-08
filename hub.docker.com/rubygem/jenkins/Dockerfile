FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.8

RUN gem install jenkins --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jenkins"]
CMD ["--help"]
