FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.9.6

RUN gem install derfred-workling --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["workling_client"]
CMD ["--help"]
