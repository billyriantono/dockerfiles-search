FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.7.4

RUN gem install cloudfactory --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cf"]
CMD ["--help"]
