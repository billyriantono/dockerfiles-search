FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install dmg --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dmg"]
CMD ["--help"]
