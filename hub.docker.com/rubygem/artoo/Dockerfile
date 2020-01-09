FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.8.2

RUN gem install artoo --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["artoo"]
CMD ["--help"]
