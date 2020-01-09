FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.4

RUN gem install echi-converter --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["echi-converter"]
CMD ["--help"]
