FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.2

RUN gem install backzilla --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["backzilla"]
CMD ["--help"]
