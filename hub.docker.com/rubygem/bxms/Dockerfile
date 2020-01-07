FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.22

RUN gem install BxMS --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["bxms"]
CMD ["--help"]
