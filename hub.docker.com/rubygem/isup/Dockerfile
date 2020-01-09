FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0

RUN gem install isup --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["isup"]
CMD ["--help"]
