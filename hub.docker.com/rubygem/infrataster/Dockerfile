FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.2

RUN gem install infrataster --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["infrataster"]
CMD ["--help"]
