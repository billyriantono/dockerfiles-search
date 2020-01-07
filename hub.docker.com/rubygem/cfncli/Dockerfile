FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.1

RUN gem install cfncli --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cfncli"]
CMD ["--help"]
