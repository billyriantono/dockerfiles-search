FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.5

RUN gem install docrails_kindle --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["docrails_kindle"]
CMD ["--help"]
