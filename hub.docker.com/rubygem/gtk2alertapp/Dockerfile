FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.7.1

RUN gem install gtk2alertapp --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gtk2alertdaemon"]
CMD ["--help"]
