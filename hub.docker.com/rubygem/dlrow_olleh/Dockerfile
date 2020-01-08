FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.0

RUN gem install dlrow_olleh --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dlrow_olleh"]
CMD ["--help"]
