FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.9

RUN gem install docker-utils --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["docker-utils"]
CMD ["--help"]
