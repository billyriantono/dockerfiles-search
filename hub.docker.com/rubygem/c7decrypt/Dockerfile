FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.2

RUN gem install c7decrypt --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["c7decrypt"]
CMD ["--help"]
