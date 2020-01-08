FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.8.9

RUN gem install chriseppstein-compass --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["compass"]
CMD ["--help"]
