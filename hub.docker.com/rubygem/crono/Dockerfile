FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.2

RUN gem install crono --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["crono"]
CMD ["--help"]
