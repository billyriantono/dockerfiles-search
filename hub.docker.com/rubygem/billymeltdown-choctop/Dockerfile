FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.11.0.8

RUN gem install billymeltdown-choctop --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["install_choctop"]
CMD ["--help"]
