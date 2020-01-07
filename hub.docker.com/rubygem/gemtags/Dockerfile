FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.5

RUN gem install gemtags --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gemtags"]
CMD ["--help"]
