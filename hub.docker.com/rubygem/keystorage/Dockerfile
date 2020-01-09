FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.7

RUN gem install keystorage --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["keystorage"]
CMD ["--help"]
