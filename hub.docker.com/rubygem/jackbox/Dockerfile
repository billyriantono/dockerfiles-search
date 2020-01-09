FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.6.9

RUN gem install jackbox --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jackup"]
CMD ["--help"]
