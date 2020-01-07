FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.2

RUN gem install gem2rpm --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gem2rpm"]
CMD ["--help"]
