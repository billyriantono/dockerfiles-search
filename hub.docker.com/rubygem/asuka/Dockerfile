FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.3

RUN gem install asuka --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["asuka"]
CMD ["--help"]
