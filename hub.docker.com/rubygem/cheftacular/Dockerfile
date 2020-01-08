FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.9.1

RUN gem install cheftacular --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cft"]
CMD ["--help"]
