FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.1

RUN gem install aozora4reader --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["a4r"]
CMD ["--help"]
