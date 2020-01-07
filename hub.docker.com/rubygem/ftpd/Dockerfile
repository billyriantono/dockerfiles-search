FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0.1

RUN gem install ftpd --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ftpdrb"]
CMD ["--help"]
