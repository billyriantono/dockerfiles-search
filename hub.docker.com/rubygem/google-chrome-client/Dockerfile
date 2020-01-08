FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2

RUN gem install google-chrome-client --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["chrome-repl"]
CMD ["--help"]
