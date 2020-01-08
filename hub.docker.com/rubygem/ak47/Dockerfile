FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.5

RUN gem install ak47 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ak47"]
CMD ["--help"]
