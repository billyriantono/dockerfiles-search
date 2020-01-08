FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.6

RUN gem install geminstaller --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["geminstaller"]
CMD ["--help"]
