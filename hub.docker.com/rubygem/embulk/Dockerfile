FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.8.9

RUN gem install embulk --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["embulk"]
CMD ["--help"]
