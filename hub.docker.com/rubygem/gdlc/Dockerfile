FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.1.3.1

RUN gem install gdlc --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gdlc"]
CMD ["--help"]
