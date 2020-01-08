FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.3

RUN gem install gatchaman --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gatchan"]
CMD ["--help"]
